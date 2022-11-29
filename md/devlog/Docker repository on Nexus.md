---
created: 1657898170341
desc: ''
id: ccglabj2ycmrw83mownsa6l
title: Docker repository on Nexus
updated: 1657900013774
---
   
Related::  [nexus](../devlog/nexus.md), [docker](../devlog/docker.md)   
   
   
---   
   
Let's create a Nexus repository for pushing Docker Images.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657898240/wiki/xtuuz0risepxxvasvtph.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657898250/wiki/qwzgsrveb6nnaw6mjtbv.png)   
   
Nexus will give you a URL which can be used to push the Docker Images.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657898282/wiki/uzqnzn9ytfxv5v3lepem.png)   
   
Create User role for Docker repository   
   
You need this since you’d `docker login` into the Nexus repository with the credentials provided by Nexus so you can push images to this repository.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657898401/wiki/e3ws3cnkzx3pjugcah5z.png)   
   
Assign the privilege to the role and assign that role to your Nexus User.   
   
The endpoint for `docker login` would be `ipAddres:port` you’d need the Docker repository’s port(different from the Nexus’s port).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657898631/wiki/wd2c0lpxian1nawdszqj.png)   
   
Expose the port the Nexus server’s firewall.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657898733/wiki/sf4hnvqudcdpm1latsq7.png)   
   
Configure Realm in Nexus   
   
When you do `docker login`, you get token of authentication from Nexus Docker Repository for a client, the token will be stored in the machine from where you’re pushing the images. The location of the token will be `~/.docker/config.json`.   
   
We configure the issuance of that token.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657899004/wiki/hvl6ifvbatliuxgkq9bi.png)   
   
Docker by default only allows client request to talk to an HTTPS endpoint of a Docker registry, it won’t allow an HTTP endpoint. We’ve to ask Docker to allow insecure endpoint as an exception.   
   
Configure insecure registry on Linux by editing `/etc/docker/daemon.json` and add: Ip address:port of Nexus.   
   
```json
{
  "insecure-registries": ["ipAddress:8083"]
}
```
   
   
On Docker Desktop:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657899306/wiki/dnqx8sntzibnnfofspda.png)   
   
Now you’re set for `docker login`   
   
`docker login 167.99.248.163:8083`   
   
Build an image from a `Dockerfile`   
   
Retag or rename the image itself to add the name of the repository where it is needed to be pushed.   
   
`docker tag my-image:1.0 167.99.248.163:8083/my-image:1.0`   
   
`docker push 167.99.248.163:8083/my-image:1.0`   
   
In the same way, you can pull images from it:   
   
`curl -u nexusUser:nexusPw -X GET 'http://167.99.248.163:8081/service/rest/v1/components?repository=docker-hosted`