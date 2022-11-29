---
created: 1662720168696
desc: ''
id: 388d7tp8xmm7ftl0xabke3a
title: Deploy to LKE Cluster from Jenkins
updated: 1662720168695
---
   
Related::  [LKE](../devlog/LKE.md), [jenkins](../devlog/jenkins.md), [kubernetes](../devlog/kubernetes.md)   
   
---   
We’re going to spin up a K8s cluster on LKE and deploy to it from Jenkins pipeline.   
   
There isn’t going to be any platform specific authentication unlike [aws.eks.Deploy to EKS Cluster from Jenkins](../devlog/aws.eks.Deploy%20to%20EKS%20Cluster%20from%20Jenkins.md).   
   
There are different ways of authenticating to a K8s cluster depending on platform.   
   
**Overview**   
   
   
- Install `kubectl` on Jenkins container.   
- Install K8s Cli Jenkins plugin to execute `kubectl` with kubeconfig credentials.   
- We’ll use the plugin in the Jenkinsfile and deploy it to LKE cluster.   
   
## Create cluster on LKE and connect to it   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662721037/wiki/q0o8izux0r3nnq94mroq.png)   
   
   
Download the `kubeconfig.yaml`   
   
## Provide LKE credentials to Jenkins   
   
Lets create credentials in Jenkins using `kubeconfig.yaml` so Jenkins can connect to it.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662721346/wiki/zayoahdityof5ysyvskt.png)   
   
## Install `kubectl` on Jenkins   
   
   
- SSH into the machine where Jenkins is running.   
- `docker exec -u 0 -it <container-id> bash` to go inside the container.   
- [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux) using [curl](/not_created.md)   
- `chmod +x ./kubectl`   
- `mv ./kubectl /usr/local/bin/kubectl`   
- `kubectl version`   
   
## Install Kubernetes CLI plugin on Jenkins   
   
From Manage Jenkins > Plugin Manager   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662721477/wiki/k5rvyrcxwlbk5uvf93w7.png)   
   
## Configure Jenkinsfile    
   
To deploy to LKE cluster   
   
```groovy
#!/usr/bin/env groovy

pipeline {
    agent any
    stages {
        stage('build app') {
            steps {
               script {
                   echo "building the application..."
               }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                   echo 'deploying docker image...'
                   withKubeConfig([credentialsId: 'lke-credentials', serverUrl: 'https://<API endpoint>linodelke.net']) {
                       sh 'kubectl create deployment nginx-deployment --image=nginx'
                   }
                }
            }
        }
    }
}
```
   
   
Configure the pipeline with the branch from where the Jenkinsfile is being served.   
   
Find the finished code at [Files · deploy-to-lke · zubayrrr / java-maven-app · GitLab](https://gitlab.com/zubayrrr/java-maven-app/-/tree/deploy-to-lke)