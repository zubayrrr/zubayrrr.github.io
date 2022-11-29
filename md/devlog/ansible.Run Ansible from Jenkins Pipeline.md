---
created: 1661510467420
desc: ''
id: bcv6bt39npyppdge84l270c
title: Run Ansible from Jenkins Pipeline
updated: 1661512241276
---
   
Topics::  [jenkins](../devlog/jenkins.md)   
   
   
---   
   
Let's integrate Ansible in Jenkins, execute a Playbook inside Jenkins pipeline.   
   
**Overview**   
   
1. Create a DO server for Jenkins   
2. Create dedicated server for Ansible   
3. Install Ansible on that server   
   
   
   - Run Ansible locally on Jenkins   
   - Or have a dedicated server for Ansible   
   
4. Execute Ansible Playbook from Jenkins Pipeline (by   
   creating Jenkinsfile that executes Playbook on the   
   remote Ansible server)   
   
**Steps**:   
   
   
- Create 2 EC2 instances.   
- Configure everything from scratch with Ansible.   
- Create a pipeline in Jenkins.   
- Connect pipeline to a [languages.java](../devlog/languages.java.md) Maven app.   
- Create Jenkinsfile that executes Ansible Playbook on the remote Ansible server(from Jenkins), Playbook will basically configure the [aws.EC2](../devlog/aws.EC2.md) instances by installing [docker](../devlog/docker.md) and `docker-compose` on them.   
   
**Prepare Ansible Control Node**   
   
   
- Create a [DigitalOcean](../devlog/digitalocean.md) Droplet.   
- [SSH](../devlog/ssh.md) into the droplet and install Ansible on it.   
  - Also install the [languages.Python](../devlog/languages.python.md) module i.e, [boto](../devlog/boto.md) and `botocore` for AWS.   
  - Check if `pip3` is installed.   
  - `pip3 install boto3 botocore`   
- Configure AWS credentials on the Ansible server for [ansible.dynamic inventory](../devlog/ansible.dynamic%20inventory.md).   
  - `~/.aws/credentials`   
   
**Create 2 EC2**   
   
To be managed by Ansible.   
   
   
- Create them from the AWS management console.   
- Create SSH key pair and download it so you can provide it to Ansible.   
   
**Prepare Jenkinsfile**   
   
To copy files from Jenkins to Ansible server.   
   
We need to copy 4 files in total to Ansible server from the server on which Jenkins pipeline is running.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661512294/wiki/ewykps4znh822pxabsp7.png)   
   
   
   
- The first stage would be using `sshagent` plugin in Jenkins to copy the files to a remote server.   
- We also need to pass it the SSH key (for the remote server we’re trying to copy files to).   
- You can add this credentials to Jenkins with “SSH Username with private key”.   
- You can convert it to the old format using `ssh-keygen -p -f ~/.ssh/id_rsa -m pem -P "" -N ""`   
- We also need the `.pem` files to be added as a credentials on Jenkins for the EC2 instances so the key can be copied from the EC2 to Ansible server which will use the provided keys to connect to both the servers.   
   
   
- The second stage will execute the playbook which will configure the EC2 instances.   
- We’re using [ssh-steps-plugin: Jenkins pipeline steps which provides SSH facilities such as command execution or file transfer for continuous delivery.](https://github.com/jenkinsci/ssh-steps-plugin).   
   
```groovy
pipeline {
    agent any
    environment {
        ANSIBLE_SERVER = "167.99.136.157"
    }
    stages {
        stage("copy files to ansible server") {
            steps {
                script {
                    echo "copying all neccessary files to ansible control node"
                    sshagent(['ansible-server-key']) {
                        sh "scp -o StrictHostKeyChecking=no ansible/* root@${ANSIBLE_SERVER}:/root"

                        withCredentials([sshUserPrivateKey(credentialsId: 'ec2-server-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]) {
                            sh 'scp $keyfile root@$ANSIBLE_SERVER:/root/ssh-key.pem'
                        }
                    }
                }
            }
        }
        stage("execute ansible playbook") {
            steps {
                script {
                    echo "calling ansible playbook to configure ec2 instances"
                    def remote = [:]
                    remote.name = "ansible-server"
                    remote.host = ANSIBLE_SERVER
                    remote.allowAnyHosts = true

                    withCredentials([sshUserPrivateKey(credentialsId: 'ansible-server-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                        remote.user = user
                        remote.identityFile = keyfile
                        sshScript remote: remote, script: "prepare-ansible-server.sh"
                        sshCommand remote: remote, command: "ansible-playbook my-playbook.yaml"
                    }
                }
            }
        }
    }   
}

```
   
   
```bash
#!/usr/bin/env bash

# prepare-ansible-server.sh


apt update
apt install ansible -y
apt install python3-pip -y
pip3 install boto3 botocore
```
   
   
**Create Jenkins Pipeline**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661513949/wiki/jwejfe9vgpjcmpj3wewr.png)   
   
You can find the finished code at [Files · feature/ansible · zubayrrr / java-maven-app · GitLab](https://gitlab.com/zubayrrr/java-maven-app/-/tree/feature/ansible)