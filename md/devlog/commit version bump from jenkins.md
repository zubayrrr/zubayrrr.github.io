---
created: 1660687142297
desc: ''
id: tov33lpu7q398bhlhxc0smh
title: Commit Version Bump from Jenkins
updated: 1660729348293
---
   
Update the version bump of the `pom.xml` to the remote repository.   
   
Add another stage:   
   
```groovy
stage("commit version update") {
  steps {
    script {
      withCredentials([usernamePassword(credentialsId: 'gitlab-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
        sh 'git config --global user.email "jenkins@example.com"'
        sh 'git config --global user.name "jenkins"'
        sh 'git status'
        sh 'git branch'
        sh 'git config -l'
        sh "git remote set-url origin https://${USER}:${PASS}@gitlab.com/user/repo.git"
        sh 'git add .'
        sh 'git commit -m "version bump"'
        sh 'git push origin HEAD:jenkins-job'
      }
    }
  }
}
```
   
   
## Ignore Jenkins commit for Jenkins pipeline trigger   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660729401/wiki/uxjn1qhpaykw3kdin9hj.png)   
   
To avoid this:    
   
We need to detect that the commit was made by Jenkins user and not the developers and ignore the trigger for that commit.   
   
We can do this by installing “Ignore Committer Strategy” plugin.   
   
Once installed, “Build strategies” option will appear in the config of the pipeline.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660733313/wiki/rwkgbpplihk09sije8eb.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660733332/wiki/wognrezymwta43kq6dls.png)