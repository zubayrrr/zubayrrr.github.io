---
created: 1662681055011
desc: ''
id: jy7mksy4wj1448sv97qgw56
title: ECR
updated: 1662681086221
---
   
It is simply a repository for container images. It is an alternative to Nexus, DockerHub   
   
Integrates well with other AWS services   
Eg: EKS with EC2 - easier to connect your cluster with ECR to fetch instances), Automatically update whenever a new version is published to registry.   
   
You basically create private repositories your application/docker images and you can start pushing different versions/tags of that images to the registries.   
   
And use the endpoint to download the images to the cluster.   
   
## Create a repository   
   
1. Create a repository on ECR   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657837712/wiki/ltcqb9ivijzbe6ztxx5m.png)   
   
2. Authenticate yourself with `docker login` in AWS ECR’s case, it’ll give you an `aws` cli command that uses `docker login` in the background.   
   
3. ![](https://res.cloudinary.com/zubayr/image/upload/v1657837868/wiki/imnm6ysoqpfjh9xli9xv.png)