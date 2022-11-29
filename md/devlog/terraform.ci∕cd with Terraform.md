---
created: 1661525048278
desc: ''
id: hps5pi009ekind40nvvo8wy
title: CI∕CD with Terraform
updated: 1661537027444
---
   
**Overview**   
   
Let's integrate [terrform](/not_created.md) into our CI/CD pipeline.   
   
We'll begin from [Files · feature/jenkinsfile-sshagent · zubayrrr / java-maven-app · GitLab](https://gitlab.com/zubayrrr/java-maven-app/-/tree/feature/jenkinsfile-sshagent)   
   
We'll be automating provisioning.   
   
Right now, we're hard coding the address of the EC2 instance since we created it manually but we want to integrate Terraform in this process by dynamically starting an instance(provision) and then deploy our app.   
   
We'll add a new stage to our Jenkinsfile to provision a new server. **The steps**:   
   
   
- Creating an [ssh](../devlog/ssh.md) key pair   
- Install Terraform in the Jenkins container because we'll be executing Terraform commands inside the stage (we could use Jenkins Terraform plugin but commands are easier to use).   
- Write Terraform code(configuration files will be part of application code).   
   
**Create Key Pair**   
   
   
- Create key pair from AWS management console and download it and give to Jenkins.   
  - Create a new credentials in Jenkins with "SSH Username and private key".   
   
**Install Terraform in Jenkins container**   
   
   
- SSH into the machine from where the Jenkins is running.   
- Enter into the container as root `docker exec -it -u 0 <container-id> bash`.   
- Check your OS `cat /etc/os-release` and based on that [Install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli).   
   
**Terraform configuration**   
   
inside the application code.   
   
   
- Create a dir named "terraform" and add a `main.tf` file to get started.   
- We'll borrow code from [main.tf · zubayrrr/terraform-learn · GitLab](https://gitlab.com/zubayrrr/terraform-learn/-/blob/feature/deploy-to-ec2-default-components/main.tf) as a starting point and adjust the code for our needs.   
   
```tf
terraform {
    required_version = ">= 0.12"
    backend "s3" {
        bucket = "myapp-bucket"
        key = "myapp/state.tfstate"
        region = "eu-west-3"
    }
}

provider "aws" {
    region = var.region
}

resource "aws_vpc" "myapp-vpc" {
    cidr_block = var.vpc_cidr_block
    tags = {
        Name: "${var.env_prefix}-vpc"
    }
}

resource "aws_subnet" "myapp-subnet-1" {
    vpc_id = aws_vpc.myapp-vpc.id
    cidr_block = var.subnet_cidr_block
    availability_zone = var.avail_zone
    tags = {
        Name: "${var.env_prefix}-subnet-1"
    }
}

resource "aws_internet_gateway" "myapp-igw" {
    vpc_id = aws_vpc.myapp-vpc.id
    tags = {
        Name: "${var.env_prefix}-igw"
    }
}

resource "aws_default_route_table" "main-rtb" {
    default_route_table_id = aws_vpc.myapp-vpc.default_route_table_id

    route {
        cidr_block = "0.0.0.0/0"
        gateway_id = aws_internet_gateway.myapp-igw.id
    }
    tags = {
        Name: "${var.env_prefix}-main-rtb"
    }
}

resource "aws_default_security_group" "default-sg" {
    vpc_id = aws_vpc.myapp-vpc.id

    ingress {
        from_port = 22
        to_port = 22
        protocol = "tcp"
        cidr_blocks = [var.my_ip, var.jenkins_ip]
    }

    ingress {
        from_port = 8080
        to_port = 8080
        protocol = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
    }

    egress {
        from_port = 0
        to_port = 0
        protocol = "-1"
        cidr_blocks = ["0.0.0.0/0"]
        prefix_list_ids = []
    }

    tags = {
        Name: "${var.env_prefix}-default-sg"
    }
}

data "aws_ami" "latest-amazon-linux-image" {
    most_recent = true
    owners = ["amazon"]
    filter {
        name = "name"
        values = ["amzn2-ami-hvm-*-x86_64-gp2"]
    }
    filter {
        name = "virtualization-type"
        values = ["hvm"]
    }
}

resource "aws_instance" "myapp-server" {
    ami = data.aws_ami.latest-amazon-linux-image.id
    instance_type = var.instance_type

    subnet_id = aws_subnet.myapp-subnet-1.id
    vpc_security_group_ids = [aws_default_security_group.default-sg.id]
    availability_zone = var.avail_zone

    associate_public_ip_address = true
    key_name = "myapp-key-pair"

    user_data = file("entry-script.sh")

    tags = {
        Name = "${var.env_prefix}-server"
    }
}

output "ec2_public_ip" {
    value = aws_instance.myapp-server.public_ip
}
```
   
   
We'll also need to add `entry-script.sh` to the `terraform` dir.   
   
```sh
#!/bin/bash
sudo yum update -y && sudo yum install -y docker
sudo systemctl start docker
sudo usermod -aG docker ec2-user

# install docker-compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
   
   
Make sure you also copy the variables from `terraform.tfvars` to a new file in `./terraform/variables.tf`. Define default values for those variables whose values don't change often.   
   
**Provision stage in Jenkins**   
   
and   
   
**Deploy stage**   
   
```groovy
#!/usr/bin/env groovy

library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [$class: 'GitSCMSource',
     remote: 'https://gitlab.com/nanuchi/jenkins-shared-library.git',
     credentialsId: 'gitlab-credentials'
    ]
)

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    environment {
        IMAGE_NAME = 'nanajanashia/demo-app:java-maven-2.0'
    }
    stages {
        stage('build app') {
            steps {
               script {
                  echo 'building application jar...'
                  buildJar()
               }
            }
        }
        stage('build image') {
            steps {
                script {
                   echo 'building docker image...'
                   buildImage(env.IMAGE_NAME)
                   dockerLogin()
                   dockerPush(env.IMAGE_NAME)
                }
            }
        }
        stage('provision server') {
            environment {
                AWS_ACCESS_KEY_ID = credentials('jenkins_aws_access_key_id')
                AWS_SECRET_ACCESS_KEY = credentials('jenkins_aws_secret_access_key')
                TF_VAR_env_prefix = 'test'
            }
            steps {
                script {
                    dir('terraform') {
                        sh "terraform init"
                        sh "terraform apply --auto-approve"
                        EC2_PUBLIC_IP = sh(
                            script: "terraform output ec2_public_ip",
                            returnStdout: true
                        ).trim()
                    }
                }
            }
        }
        stage('deploy') {
            environment {
                DOCKER_CREDS = credentials('docker-hub-repo')
            }
            steps {
                script {
                   echo "waiting for EC2 server to initialize"
                   // you can also make the "provision server" as the first stage
                   sleep(time: 90, unit: "SECONDS")

                   echo 'deploying docker image to EC2...'
                   echo "${EC2_PUBLIC_IP}"

                   def shellCmd = "bash ./server-cmds.sh ${IMAGE_NAME} ${DOCKER_CREDS_USR} ${DOCKER_CREDS_PSW}"
                   def ec2Instance = "ec2-user@${EC2_PUBLIC_IP}"

                   sshagent(['server-ssh-key']) {
                       sh "scp -o StrictHostKeyChecking=no server-cmds.sh ${ec2Instance}:/home/ec2-user"
                       sh "scp -o StrictHostKeyChecking=no docker-compose.yaml ${ec2Instance}:/home/ec2-user"
                       sh "ssh -o StrictHostKeyChecking=no ${ec2Instance} ${shellCmd}"
                   }
                }
            }
        }
    }
}

```
   
   
Make sure Jenkins IP is allowed to access port 22 on the EC2 instances (check `./terraform/variables`).   
   
For Docker login(to access the private repo) we'll use:   
   
```sh
#!/usr/bin/env bash

# server-cmds.sh

export IMAGE=$1
export DOCKER_USER=$2
export DOCKER_PWD=$3
echo $DOCKER_PWD | docker login -u $DOCKER_USER --password-stdin
docker-compose -f docker-compose.yaml up --detach
echo "success"

```
   
   
**To destroy**   
   
Run `terraform destroy` as a stage in the Jenkinsfile and run a job.   
   
The finished code can be found at [zubayrrr / java-maven-app · GitLab](https://gitlab.com/zubayrrr/java-maven-app/-/tree/feature/sshagent-terraform/)