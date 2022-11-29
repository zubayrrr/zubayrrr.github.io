---
created: 1655214372438
desc: ''
id: 49naltrgmfezkzp9g3fjfaq
title: AWS CodeDeploy
updated: 1655535050036
---
   
It is a service offered by Amazon that is used for the purpose of deployment. It helps in the automation of the application deployment of Amazon EC2 instances, on premise instances, [serverless](../devlog/serverless.md) Lambda functions, and [AWS ECS](../devlog/AWS%20ECS.md) services.   
   
You can also deploy to hundreds to [aws.EC2](../devlog/aws.EC2.md) instances across multiple regions(EC2 Placement Group).   
   
## Get started   
   
Provision an IAM user with access to CodeDeploy, attach CodeDeploy policy to the user or to the group or create a role for your [aws.EC2](../devlog/aws.EC2.md)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655276802/wiki/wzyhpfgy8jpfirpdnbsx.png)   
   
Also create a role for AWS CodeDeploy   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655276831/wiki/kr76xkzjndcvvdrkrzjx.png)   
   
Make sure your roles have necessary policies attached.   
   
Before creating any instances, make sure you create a [load balancer](../devlog/load%20balancer.md) for your EC2 Instances.   
   
   
- We deploy **Revisions**   
- How to deploy and rate of deployment is informed by **Deployment Configuration**   
- We deploy to a **Deployment Group**(one or more EC2 Instances)   
   
Also create an [aws.IAM](../devlog/aws.IAM.md) **instance profile** to allow EC2 to access your repositories.   
   
Create an IAM service role that will grant CodeDeploy access to other AWS resources.   
   
### Application on CodeDeploy   
   
It is simply a name identifier used to reference your deployment settings.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655279039/wiki/hxyajjgibg8e0p40uyjp.png)   
   
### Deployment group   
   
It is the instance or instances where you want to target and deploy your code(these can be anything like [aws.EC2](../devlog/aws.EC2.md), [AWS Lambda](../devlog/AWS%20Lambda.md), On-prem)   
   
Set of individual instances targeted for a deployment.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655279075/wiki/wniwxneyipowixraaycf.png)   
   
Use [AWS Route53](../devlog/AWS%20Route53.md) to point your domain to the load balancer.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655279389/wiki/mccbiihnndd3o8uhi9fs.png)   
   
### Deployment Configuration   
   
It is a set of rules, success and failure conditions used by CodeDeploy for deployment.   
   
It uses minimum healthy host value to determine what percentage of instances need to be up all the time from the configuration file.   
   
To add automation we can bring in:   
   
   
- [AWS EventBridge](../devlog/AWS%20EventBridge.md) - monitor deployment   
- [AWS SNS](/not_created.md) - subscribe to SNS topic for notifications(email)   
- [AWS Lambda](../devlog/AWS%20Lambda.md) - to get instant/immediate updates on deployment (Slack)   
   
We can automate redeployment or rollback based on the result of our deployment.   
   
Default deployment options are:   
   
   
- One at a time   
- All at once   
- Half at a time   
   
### `appspec.yml` file   
   
`appspec.yml` is the file that has all the instructions for the deployment process.   
   
It is used to manage each deployment as a series of lifecycle event hooks (much like [AWS Auto Scaling Group](../devlog/AWS%20Auto%20Scaling%20Group.md)). These event hooks are defined in the file.   
   
```yaml
# appspecstub.yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html/WordPress
hooks:
  BeforeInstall:
    - location: scripts/install_dependencies.sh
      timeout: 300
      runas: root
  AfterInstall:
    - location: scripts/change_permissions.sh
      timeout: 300
      runas: root
  ApplicationStart:
    - location: scripts/start_server.sh
    - location: scripts/create_test_db.sh
      timeout: 300
      runas: root
  ApplicationStop:
    - location: scripts/stop_server.sh
      timeout: 300
      runas: root
```
   
   
### Revision   
   
A revision refers to the bundle (zip, tar files) containing the current group of files you want to deploy. It could be an update, bug fixes, deployment for the first time.   
   
### Lifecycle Event Hooks   
   
The hooks allow you to run custom code at various time during deployment(BeforeInstall, AfterInstall).   
   
## Resources   
   
   
- [Working with deployment configurations in CodeDeploy - AWS CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployment-configurations.html)