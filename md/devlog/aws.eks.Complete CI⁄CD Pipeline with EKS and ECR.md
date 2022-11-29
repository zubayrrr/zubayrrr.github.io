---
created: 1662727398180
desc: ''
id: 37kqj94evwjjel399caht4l
title: Complete CI⁄CD Pipeline with EKS and ECR
updated: 1662727854895
---
   
Related::  [kubernetes](../devlog/kubernetes.md), [aws.ecr](../devlog/aws.ecr.md)   
   
   
---   
![](https://res.cloudinary.com/zubayr/image/upload/v1662727470/wiki/atvyvdxb7h7m27l5kymd.png)   
   
In [aws.eks.Complete CI⁄CD Pipeline with EKS and DockerHub](../devlog/aws.eks.Complete%20CI%E2%81%84CD%20Pipeline%20with%20EKS%20and%20DockerHub.md) we pushed Images to DockerHub after building. Let’s do the same but with [aws.ecr](../devlog/aws.ecr.md) instead.   
   
**Overview**   
   
   
- Create ECR repo.   
- Create credentials in Jenkins.   
- Adjust building and tagging.   
- Create Secret for ECR.   
   
   
## Create ECR repository   
   
From management console, create a new private ECR repository.   
   
## Create credentials in Jenkins   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662727966/wiki/veesvytneaawnjylufq3.png)   
   
Use the commands provided by clicking on “View push commands”, once you’ve the password, copy it   
   
## Create Secret for ECR   
   
```
kubectl create secret docker-registry aws-registry-key \
--docker-server=<docker-server-url>
--docker-username=AWS \
--docker-password= <password> # aws ecr get-login-password
```
   
   
## Jenkinsfile, Deployment and Service   
   
```groovy
#!/usr/bin/env groovy

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    environment {
        ECR_REPO_URL = '664574038682.dkr.ecr.eu-west-3.amazonaws.com'
        IMAGE_REPO = "${ECR_REPO_URL}/java-maven-app"
    }
    stages {
        stage('increment version') {
            steps {
                script {
                    echo 'incrementing app version...'
                    sh 'mvn build-helper:parse-version versions:set \
                        -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                        versions:commit'
                    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version = matcher[0][1]
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                    echo "############ ${IMAGE_REPO}"
                }
            }
        }
        stage('build app') {
            steps {
               script {
                   echo "building the application..."
                   sh 'mvn clean package'
               }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'ecr-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "docker build -t ${IMAGE_REPO}:${IMAGE_NAME} ."
                        sh "echo $PASS | docker login -u $USER --password-stdin ${ECR_REPO_URL}"
                        sh "docker push ${IMAGE_REPO}:${IMAGE_NAME}"
                    }
                }
            }
        }
        stage('deploy') {
            environment {
                AWS_ACCESS_KEY_ID = credentials('jenkins_aws_access_key_id')
                AWS_SECRET_ACCESS_KEY = credentials('jenkins_aws_secret_access_key')
                APP_NAME = 'java-maven-app'
            }
            steps {
                script {
                    echo 'deploying docker image...'
                    sh 'envsubst < kubernetes/deployment.yaml | kubectl apply -f -'
                    sh 'envsubst < kubernetes/service.yaml | kubectl apply -f -'
                }
            }
        }
        stage('commit version update') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'gitlab-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'git config user.email "jenkins@example.com"'
                        sh 'git config user.name "Jenkins"'
                        sh "git remote set-url origin https://${USER}:${PASS}@gitlab.com/zubayrrr/java-maven-app.git"
                        sh 'git add .'
                        sh 'git commit -m "ci: version bump"'
                        sh 'git push origin HEAD:jenkins-jobs'
                    }
                }
            }
        }
    }
}
```
   
   
```yaml
# kubernetes/deployment.ymal
apiVersion: apps/v1
kind: Deployment
metadata:
  name: $APP_NAME
  labels:
    app: $APP_NAME
spec:
  replicas: 1
  selector:
    matchLabels:
      app: $APP_NAME
  template:
    metadata:
      labels:
        app: $APP_NAME
    spec:
      imagePullSecrets:
        - name: my-registry-key
      containers:
        - name: $APP_NAME
          image: $IMAGE_REPO:$IMAGE_NAME
          imagePullPolicy: Always
          ports:
            - containerPort: 8080
```
   
   
```yaml
# kubernetes/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: $APP_NAME
spec:
  selector:
    app: $APP_NAME
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```
   
   
## Execute Jenkins Pipeline   
   
Commit the changes and on trigger a job.