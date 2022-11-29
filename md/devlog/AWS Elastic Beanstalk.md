---
created: 1655546329187
desc: ''
id: 9nmlp83ktbytu4zbkdl7o0d
title: AWS Elastic Beanstalk
updated: 1655629643197
---
   
Elastic Beanstalk is a platform within AWS that is used for deploying and scaling web applications. In simple terms this platform as a service (PaaS) takes your application code and deploys it while provisioning the supporting architecture and compute resources required for your code to run. Elastic Beanstalk also fully manages the patching and security updates for those provisioned resources.   
   
There is no charge to use Elastic Beanstalk to deploy your applications, you are only charged for the resources that are created to support your application.   
   
AWS Elastic Beanstalk allows you to quickly deploy applications and services without having to worry about configuring underlying resources, services, operating systems or web servers.   
   
Elastic Beanstalk takes care of the hosting infrastructure, coding language interpreter, operating system, security, https service and application layer. All you need to worry about is writing your code.   
   
You can develop code in a number of languages which is then zipped up and the zip file is used when instantiating a new elastic beanstalk instance.   
   
   
- via [What is AWS Elastic Beanstalk?](https://www.hava.io/blog/what-is-aws-elastic-beanstalk)   
   
When we create an Elastic Beanstalk environment , underneath it, we’re creating CloudFormation stack. We have the option of having Elastic Beanstalk within a CloudFormation template.   
   
## Application   
   
It is a collection of components, environments, versions, configurations   
   
## Upload version   
   
Upload artifact, source bundle a zip, tar, war, jar file.   
   
## Environment   
   
A collection of AWS resources running application version.   
   
## Manage   
   
For updating the application, you simply upload a new version and the rest is again taken care by Elastic Beanstalk.   
   
## Elastic Beanstalk VS [AWS OpsWorks](../devlog/AWS%20OpsWorks.md) VS [aws.CloudFormation](../devlog/aws.CloudFormation.md)   
   
   
- Elastic Beanstalk is geared towards developers and is the simplest to use but provides the least visibility of whats going on "under the hood". You can quickly deploy applications. It is great for testing. If you have a lot of dependencies and a complicated deployment process Elastic Beanstalk not be the best choice.   
- OpsWorks is a configuration management services that provides managed instances of [chef](../devlog/chef.md) and [puppet](../devlog/puppet.md). Great for hybrid environments because if node is reachable by Chef or Puppet instances(On-prem), it can be registered with OpsWorks.   
- CloudFormation compared to Elastic Beanstalk deals more with AWS infrastructure rather than applications. It is geared towards system engineers, CloudFormation uses templates to create, replicate AWS infrastructure stacks rather than applications.   
   
### How to use all three together?   
   
   
- CloudFormation has resource definitions for both Elastic Beanstalk  and OpsWorks, which would enable implementing both of them in CloudFormation stack.   
- Build the infrastructure with CloudFormation and manage applications with OpsWorks and Elastic Beanstalk.   
   
   
## Create an Elastic Beanstalk Application   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655629696/wiki/kgz2k1qy0gt3433reler.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655629915/wiki/qmwmq00kynqimsw13ehu.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655630013/wiki/nsvk6zntgfhyb3iw4lcm.png)   
   
## Elastic Beanstalk deployment strategies   
   
We’ve two environment types in Elastic Beanstalk:   
   
   
- Single instance    
	- Has elastic IP address   
	- With a auto scaling group, you can have high availability even with a single instance.   
- High availability   
	- We have a group of instances   
	- Auto scaling group   
	- Load balancer   
   
Deployment Methods   
   
   
- All at once   
	- Performs updates all at once   
	- In place deployment - infrastructure doesn’t change at all   
	- Fast and requires no DNS changes    
	- Will complicate rollback a little bit   
	- Increased down time if something goes wrong   
- Rolling   
	- Will guarantee one of the instance is up at all times   
	- When update is ongoing - they’ll be detached from the load balancer   
	- When the update is completed, they’re reattached, load balancer will perform health check(overhead)   
	- Health checks failing may lead to different instances with different versions of applications    
- Rolling/Additional batch   
	- Updates are performed on newly created instances not on live instances   
	- We double auto scaling group’s capacity so we don’t run into capacity issues   
	- Takes longer than regular update(overhead)   
	- Go with this when you can’t afford reduced capacity(downtime)   
- Immutable   
	- Instances are not changed(updated) they’re completely replaced   
	- New instances with the update is added to Auto Scaling Group and previous instances are killed(only if the new deployment is successful)   
	- Provides clean rollback   
	- Needs doubling of instances for a short time   
- Blue/Green   
	- Entire environment is cloned(Auto Scaling Group and Load Balancer)   
	- Update is deployed to the cloned environment    
	- Route53 URLs are swapped with the updated instances once deployment is successful.   
	- Prevents downtime because new resources are used   
	- Can be tested in an isolated environment    
	- Con: we’re doubling our resources, requires DNS name change   
- Canary   
	- Allows you to roll out new code/features to a subset of users as an initial test   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655632839/wiki/xxzvbggiv1zttmngmv42.png)   
   
## Elastic Beanstalk Environment configuration management    
   
   
- You can configure your Elastic Beanstalk Environment’s configuration using a fodler named `.ebextentions` inside which your config files go.   
- You can add specific settings for all of the components of your environment like taking care of dependencies, Auto Scaling Group etc.   
- We can also your configurations and load from them at a later point.   
- Changes made from CLI or console have highest precedence, next settings loaded from a saved configurations. Config files have the lowest priority.   
   
## Creating an application   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655636669/wiki/s6mi2x0zkajvbyouj4f9.png)   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655636684/wiki/wizxch0khz30rpbrik71.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655636756/wiki/hh5vkabu8g4ycn1gk48o.png)   
   
Behind the scenes, Elastic Beanstalk actually creates CloudFormation stack with the resources we specified.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655636968/wiki/inimde4i38hupldmjkbq.png)   
   
   
   
## Elastic Beanstalk Docker Deployment    
   
   
Single containers can be deployed on Elastic Beanstalk but are not ideal for multi-tiered architectures. Dockerfile is mandatory. Docker run file is optional.   
   
Multi-containers on single instances with [AWS ECS](../devlog/AWS%20ECS.md). Docker run file is mandatory. There are multiple ports to communicate with. Ideal for multi-processes applications.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655652299/wiki/f41dktgd9nrubg6ivlmm.png)   
   
## Elastic Beanstalk with [AWS RDS](../devlog/AWS%20RDS.md)   
   
You create an RDS database in your Elastic Beanstalk environment. When environment is deleted, RDS database is also deleted. It means your database is tightly coupled with your environment.   
   
But it is possible to decouple the RDS database by creating it outside of Elastic Beanstalk. Better and safer for prod. This makes it much safer and you can connect the RDS database to multiple environments.