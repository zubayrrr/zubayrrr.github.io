---
created: 1662722289198
desc: ''
id: ofwqhzw3ulluvxcaup43evh
title: Complete CI⁄CD Pipeline with EKS and DockerHub
updated: 1662727783903
---
   
Related::  [docker](../devlog/docker.md)   
   
   
---   
![](https://res.cloudinary.com/zubayr/image/upload/v1662722367/wiki/mwvekg8zrkfnwd8bgvlu.png)   
   
   
---   
   
```yaml
#!/usr/bin/env groovy

pipeline {
    agent any
    tools {
        maven 'Maven'
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
                    echo "############ demo-app"
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
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "docker build -t zubayrrr/demo-app:${IMAGE_NAME} ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push demo-app:${IMAGE_NAME}"
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
   
   
## Deployment and Service files   
   
Inside a dir  “kubernetes” in the root of your project.   
   
```yaml
# deployment.yaml
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
# service.yaml
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
   
   
## Install “gettext-base” tool on Jenkins   
   
   
- SSH into the machine where Jenkins is running.   
- `docker exec -u 0 -it <container-id> bash` to go inside the container.   
- `apt-get install gettext-base`   
	- This is the package that contains `envsubst` command.   
   
## Create Secret for DockerHub credentials   
   
We only need this secret once and we can’t have this in our pipeline as it would keep creating a secret everything it runs. We’ll instead create it on our local machine.   
   
We need to be connected to `eks` cluster so the cluster can fetch the Image from our private DockerHub repository.   
   
We need one secret per namespace and secrets should be hosted in one repository.   
   
```
kubectl create secret docker-registry my-registry-key \
--docker-server=docker.io \
--docker-username=zubayrrr \
--docker-password=<password>
```
   
   
## Execute Jenkins Pipeline   
   
Commit changes to your git repo.    
   
Configure the job with the right branch and trigger a job.   
   
Find the finished code at [Files · deploy-on-k8s · zubayrrr / java-maven-app · GitLab](https://gitlab.com/zubayrrr/java-maven-app/-/tree/deploy-on-k8s)