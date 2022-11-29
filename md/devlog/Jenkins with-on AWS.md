---
created: 1655544689873
desc: ''
id: rslamxyhwny92aooavg497t
title: Jenkins with-on AWS
updated: 1655544939384
---
   
[Jenkins](../devlog/jenkins.md) interacts with [AWS](../devlog/aws.md) via Jenkins plugins for AWS.   
   
Jenkins can be swapped for [AWS CodeBuild](../devlog/AWS%20CodeBuild.md), [AWS CodeDeploy](../devlog/AWS%20CodeDeploy.md), [AWS CodePipeline](../devlog/AWS%20CodePipeline.md).   
   
Jenkins on AWS is deployed in master/agent configuration, master and worker nodes can be on the same [aws.EC2](../devlog/aws.EC2.md) instance or you can separate them on different instances.   
   
Jenkins configuration on AWS   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655544995/wiki/wcnzxychygleak7bt98d.png)   
   
Jenkins with CodePipeline    
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655545096/wiki/gzpedykm2ghhtt3jnie3.png)