---
created: 1653569035047
desc: ''
id: gvpkbgglehtr9ej5e0uj44j
title: AWS
updated: 1664999335087
---
   
AWS is an [IaaS](../devlog/IaaS.md). AWS stands for Amazon Web Services, A cloud services platform. Collection of different computer programs/services Amazon offers to build applications and websites.   
   
AWS also refers to the IT company(subsidiary of Amazon) that created these services.   
   
## Overview   
   

   
What is the Cloud?   
   
Cloud can be loosely defined as "Someone else's computer"   
   
Cloud is a collection of services that create a platform which include:   
   
   
- Media Services   
- Databases   
- Security   
- Virtual Servers   
- Networking   
- Data Storage   
- Machine Learning   
- Analytics   
   
   
- These services come with a specific feature set aimed at making an organization's life easier by hosting these services for them in remotely.   
   
   
- You can choose where in the world you want to run these services, access them remotely and fine tune them to your requirements.   
   
   
- Saving the organization a lot of money had they hosted these services themselves.   
   
   
- [AWS](../devlog/aws.md) has over 200 services.   
   
   
- Pay-as-you-go pricing:   
   
   
  - Billed by the second for using services   
  - 60 second minimum   
  - Use 83 seconds and get charged for only 83 s   
  - [AWS Lambda](../devlog/AWS%20Lambda.md) allows you to pay per millisecond !   
   
   
- Trade "capital expense" for "variable expense"   
  - capital expense is money spent ahead to buy infrastructure   
  - In cloud, we are opting for variable expense instead of capital expense.   
- We don't need to guess capacity.   
- "Go global" in minutes.   
- Avoid undifferentiated heavy lifting.
   
   
### A brief history of AWS   
   
   
- It all started with the idea of "[IaaS](/not_created.md)".   
- AWS was first released in 2006.   
- S3 was first first service that was released.   
   
### 10,000 Foot overview (of important AWS services)   
   
   
- Compute relates to running applications or processing things with computer power, including, virtual servers and serverless computing.   
- Storage relates to services like [aws.S3](../devlog/aws.S3.md) that is used to store and retrieve data.   
- Databases relates to [AWS RDS](../devlog/AWS%20RDS.md), [AWS DynamoDB](../devlog/AWS%20DynamoDB.md) etc.   
- Migration & Transfer relates to services that help you migrate your databases from non-AWS platforms(traditional servers) to AWS and also help you sync your data.   
- Networking & Content Delivery refers to VPC. virtual private cloud, where all the services exist, there are also content delivery services such as CloudFront and DNS services like Route 53.   
- Developer Tools relates to all the tools that were made to make developer's life easier in writing software and host it on AWS, from writing code, to building and deploying to servers.   
- Robotics relates to the AWS RoboMaker service that helps with robotics application development.   
- Customer Enablement services include Support from AWS themselves.   
- Blockchain services for all your cryptocurrency and blockchain needs.   
- Satellite services include Ground Station.   
- Quantum Technologies relates to Amazon Braket that provides development environment for quantum applications and algorithms.   
- Management & Governance services helps you manage AWS, on premises infrastructure.   
- Media Services relates to all the services related to media, trans-coding audio, video etc.   
- Machine Learning services offers a wide range of applications from automatic code quality check to image recognition, automatic language translation and automatic car-driving.   
- Analytics relates to processing of large data, petabytes of data.   
- Security, Identity & Compliance offers services that help with authentication, storing passwords, automatic detection of network breaches, noncompliance with predefined security policies and firewalls.   
- Front-end Web & Mobile services which help in making websites and mobile applications.   
- AR & VR relates to Amazon Sumerian, a service for creating, running 3D AR and VR applications.   
- Applications Integrations which helps AWS services work together such as SQS.   
- Cost Management, services that help you manage your budgets and costs in AWS.   
- Customer Engagement helps you manage and engage with your customers.   
- Business Applications has services such as Chime, Amazon's video conferencing software, Alexa for business etc.   
- End User Computing offers services for users such as WorkSpaces which provides a virtual desktop that can be accessed from anywhere in the world.   
- IOT services to help you build and manage IOT devices.   
- Game Development relates to Amazon GameLift for hosting games.   
- Container services that help you package code and all its dependencies in one unit that can be run reliably any computing environment.   
   
### Regions & Availability zones   
   
   
- AWS has regions, physical locations around the world where they put their data centers which have the servers that host their services.   
- Currently AWS has regions in North America, South America, Europe, the Middle East, Africa and the Asia Pacific.   
- Inside regions we've availability zones, each region has isolated and multiple availability zones in geographic area, they all have their own power, security and they're all connected to each other via redundant, ultra high speed, and low latency networks.   
- Availability zone names are randomly generated for each AWS user, example: what could be ap-southeast-2a for you will be something else for another user, like ap-southeast-2c, this is done to ensure people utilize all of their availability zones.   
- This is also done for redundancy, so that if a problem occurs at one data center, you will not be effected by it. To avoid a single point of failure. Its unlikely all of their availability zones will be hit by power cut or other such infrastructure issues.   
   
## Security and Identity   
   
   
- One of the most important things to keep in mind when building cloud applications is that your data and infrastructure is protected all times and any threats against them are being protected.   
- Coming to Identity, you've to make sure that those who do have access to your infrastructure can only access what they need to access.   
- AWS has various ways to implement Security & Identity, which can be used in different ways to do different things.   
   
### Data protection:   
   
   
- A service to discover and protect your sensitive data is Amazon Macie.   
- A service to store and manage encryption keys is AWS Key Management.   
- A service for hardware-based key storage and regulatory compliance is AWS CloudHSM.   
- A service to provision, manage and deploy SSL and TLS security certificates, is AWS Certificate Manager.   
- A service to store and retrieve secrets like passwords is [AWS Secrets Manager](../devlog/AWS%20Secrets%20Manager.md).   
   
### Infrastructure protection:   
   
   
- [aws.IAM](../devlog/aws.IAM.md) - Identity and Access Management is a way to manage who can access what throughout your AWS resources and services in your account.   
- A service for denial of service protection is AWS Shield.   
   
   
- A service to filter malicious website traffic is AWS Web Application Firewall or WAF.   
   
   
- A service to centrally manage firewall rules is AWS Firewall Manager.   
   
### Threat Detection:   
   
   
- A service that automatically detects threats is Amazon Guard Duty.   
- A service to analyze application security is Amazon Inspector.   
- A service to record and evaluate configurations of AWS resources is AWS Config.   
- A service to track user activity and API usage in your AWS account is AWS Cloudtrail.   
   
### Identity Management:   
   
   
- A service to securely manage access to your AWS account services and resources is AWS Identity and Access Management or [aws.IAM](../devlog/aws.IAM.md).   
- A service to implement cloud single sign-on is AWS Single Sign-on.   
- A service to manage identity inside your applications that you've made such as users logging in is Amazon Cognito.   
- A service to implement and manage Microsoft Active Directory is AWS Directory Service.   
- A service to centrally govern and manage multiple AWS accounts in one place is AWS Organizations.   
   
   
---   
   
   
- [Amazon VPC](../devlog/Amazon%20VPC.md) - Virtual Private Cloud is a way to organize your AWS resources into virtual private networks.   
  - Subnets, Network ACL.   
  - [Control traffic to subnets using Network ACLs - Amazon Virtual Private Cloud](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html)   
- [CIDR Blocks](/not_created.md) - CIDR blocks are used to define the (a range) IP addresses that are allowed to access your AWS resources.   
  - [Subnet Calculator - CIDR - IP ADDRESS CALCULATOR - MxToolbox](https://mxtoolbox.com/subnetcalculator.aspx)   
- Security group   
- Firewall rules   
- Subnets   
   
   
---   
   
## Compute   
   
   
- AWS describe their own compute capability as compute for any workload, instances, containers and serverless computing.   
- Compute refers to using a computer to processing something, from adding numbers to hosting multi availability zone multi-region fault tolerant version of any kind of applications.   
- This is where the processing happens.   
   
### Computing services AWS offers:   
   
   
- Instances   
  - [aws.EC2](../devlog/aws.EC2.md) or Elastic Compute Cloud refers to instances or virtual machines, a service that provides secure and resizeable virtual machines in the cloud.   
  - A service that helps you run fault tolerant workloads for up to 90% of the time for the normal price of EC2 is Amazon EC2 Spot.   
  - A service which can automatically add or remove computing capacity to meet your changes in computing demand is called Amazon EC2 Auto Scaling.   
  - A service that provides an easy to use cloud platform to build an application or website is called Amazon LightSail.   
- [containers & images](../devlog/containers%20%26%20images.md)   
  - A service to run reliable, secure and scalable containers is Amazon Elastic Container or [AWS ECS](../devlog/AWS%20ECS.md).   
  - A service to store manage and deploy container images is Amazon Elastic Registry or [AWS ECR](/not_created.md).   
  - A full managed [Kubernetes](../devlog/kubernetes.md) service is Amazon Elastic Kubernetes Service or [aws.EKS](../devlog/aws.EKS.md).   
- Serverless   
  - A service that lets you run code without servers is AWS Lambda.   
- Edge   
  - A service called AWS Outposts lets you run your AWS services on your own servers instead of Amazon's.   
  * A service that lets you bring a lot of data into AWS is called the AWS Snow Family. Devices that you can order to put files into that will be shipped back to Amazon and loaded into your AWS account.   
  * A service which lets you access AWS services from 5G devices without having to go via the internet is AWS Wavelength.   
  * A service that assists in migrating your VMware workloads to AWS is called VMware Cloud on AWS.   
  * A service that lets you run latency sensitive applications closer to end users is called AWS Local Zones.   
   
   
---   
   

   
You use AWS Cli if you want programmatic access to your AWS resources. You can execute commands from other AWS services.   
   
The AWS Cli is a very powerful command line tool. It provides commands for every AWS service and resources. Anything you can do with AWS Console can be achieved using the AWS Cli. It is also generally much easier to use AWS via the Cli than it is using the UI.   
   
## Install and Configure   
   
   
- [Installing or updating the latest version of the AWS CLI - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)   
- The default configuration is stored `~/.aws/config` and user credentials are stored in `~/.aws/credentials`.   
- The access to AWS is configured through an Access ID and Secret Access Key(which is created from the console).   
- `aws configure` to start configuring the Cli.   
- The default output format refers to the output(return) that AWS gives after running a command. This can be set as `json`.   
   
## Command Structure   
   
`aws <command> <subcommand> [options and parameters]`   
   
   
- `aws` = the base call to the AWS Cli program.   
- `command` = the AWS service   
- `subcommand` = specifies which operation to perform.   
   
Examples:   
   
   
- `aws ec2 help`   
- `aws iam help`   
   
```bash
# launch ec2 instance in the specified subnet of a VPC
aws ec2 describe-subnets
aws ec2 describe-instances # -> will give us ami-imageid, we will use the same one
aws ec2 run-instances \
    --image-id ami-xxxxxxxx \
    --count 1 \ # how many instances to launch
    --instance-type t2.micro \
    --key-name MyKeyPair \ # pem file, you can reuse thats already created or create a new one
    --security-group-ids sg-903004f8 \ # reuse already created or create a new one
    --subnet-id subnet-6e7f829e
```
   
   
## Create an EC2 Instance   
   
Steps:   
   
   
- Create a security group.   
- Create an [SSH](../devlog/ssh.md) key pair (to SSH into the created EC2 instance).   
- Create a EC2 instance.   
   
Let's start with creating a security group:   
   
   
- `aws ec2 describe-security-groups` - list all security groups   
   
> Since security group needs to be created inside a VPC, we need a VPC ID to create a new security group.   
   
   
- `aws ec2 describe-vpcs` - get all existing VPCs   
- `aws ec2 create-security-group --group-name my-sg --description "my security group" --vpc-id <vpc id>` - create a new security group.   
- `aws ec2 describe-security-groups --group-ids <security group id>` - get info on an existing SG with ID.   
   
> Configure firewall rules   
   
```bash
aws ec2 authorize-security-group-ingress \
--group-id <SG id> \
--protocol tcp \
--port 22 \
--cidr <IP addr>  # source, check your IP address, who can access
```
   
   
By default security group has outbound permissions to all destinations.   
   
> Create Key pair   
   
```
aws ec2 create-key-pair \
--key-name MyKPCli \
--query 'KeyMaterial' \ # gives unencrypted pem
--output text > MyKPCli.pem
```
   
   
> Get image-id, subnet-id   
   
   
- `aws ec2 describe-subnets` grab it either from the console or using this command   
- `aws ec2 ` grab it from the console, from the list of AMIs   
   
> Create an EC2 instance   
   
```bash
aws ec2 run-instances \
    --image-id ami-xxxxxxxx \
    --count 1 \
    --instance-type t2.micro \
    --key-name MyKPCli \
    --security-group-ids <SG ID> \
    --subnet-id <subnet ID>
```
   
   
> Grab public IP so you can SSH into it   
   
`aws ec2 describe-instances` list all instances in your region, grab the public IP from the output.   
   
> Change permissions of the .pem file   
   
   
- `ls -l MyKPCli.pem` get info on permission of this file.   
- `chmod 400 MyKPCli.pem` to modify the permissions to restrict it to only your user.   
  - Read access only for the owner.   
   
> SSH into the machine   
   
`ssh -i MyKPCli.pem ec2-user@<public-ip>`   
   
   
---   
   
## Filter & Query   
   
**Filter** and **Query** - describe command's option   
   
`aws <command> describe-` helps you with listing certain components of a resource etc.   
   
You can chain a filter to this command to filter **certain components/resource**.   
   
You can also query(s) filter attributes of a filtered **component's specific attributes**.   
   
**Examples**:   
   
```bash
aws ec2 describe-instances \
--filters "Name=instance-type, Values=t2.micro" \
--query "Reservations[].Instances[].InstanceId"
```
   
   
Even tags can also be filtered.   
   
```bash
aws ec2 describe-instances --filters "Name=tag:Type,Values=Web Server with Docker"
```
   
   
OR   
   
```bash
aws ec2 describe-instances \
--filters "Name=tag:Type,Values=Web Server with Docker" \
--query "Reservations[].Instances[].InstanceId"
```
   
   
   
---   
   
## Using IAM Command   
   
Create User, Group and assign permissions.   
   
> Create a group   
   
`aws iam create-group --group-name MyGroupCli` - the group names should sufficiently descriptive.   
   
ARN = Amazon Resource Name; to uniquely identify a component/resource. It is basically a unique **identifier**.   
   
> Create a user   
   
`aws iam create-user --user-name MyUserCli`   
   
> Add user to group   
   
`aws iam add-user-to-group --user-name MyUserCli --group-name MyGroupCli`   
   
> Get group info   
   
`aws iam get-group --group-name MyGroupCli`   
   
> Get policy ARN   
   
A policy is basically a **group of permissions**.   
   
**From Console**:   
   
Go to the IAM, click on "Policies" on the left sidebar. Click a policy to open it's summary page. Copy the **Policy ARN**.   
   
**From Cli**:   
   
You need to know the name of the policy.   
   
```bash
aws iam list-policies \
--query 'Policies[?PolicyName==`AmazonEC2FullAccess`].{ARN:arn}'
--output text
```
   
   
> Assign permissions to group   
   
Permissions can be assigned directly to a user but if you've a group of users that need same permissions it makes sense to group the users into a group and assign the permissions directly to the group.   
   
   
- `aws iam attach-user-policy`   
- `aws iam attach-group-policy`   
   
```bash
aws iam attach-group-policy \
--group-name MyGroupCli \
--policy-arn arn:aws:iam::aws:policy/AmazonEC2FullAccess
```
   
   
> Validate policy attachment   
   
```bash
aws iam list-attached-group-policies \
--group-name MyGroupCli
```
   
   
## Create Credentials   
   
**For new User**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661087467/wiki/zvzaf7d2terov8xv4owm.png)   
   
When creating a user from the console you can setup all kinds of credentials/permissions for the user.   
   
How do we do that same with the Cli?   
   
> Assign a password   
   
```bash
aws iam create-login-profile \
--user-name MyUserCli \
--password myPwd123Test \ # password needs to be strong
--password-reset-required # make user reset password on first login
# iam:ChangePassword policy needs to be attached to allow the user to change password
```
   
   
> Get user info   
   
`aws iam get-user --user-name MyUserCli` - `Account ID or ARN` will be required for the user login(Sign in as IAM User).   
   
## Create and Assign Custom Policy   
   
A custom policy for a user/group needs to be defined in a `.json` file.   
   
```json
// changePwdPolicy.json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iam:GetAccountPasswordPolicy",
      "Resource": "**"
    },
    {
      "Effect": "Allow",
      "Action": "iam:ChangePassword",
      "Resource": "arn:aws:iam::<12-digit-account-id:user/${aws:username}"
    }
  ]
}
```
   
   
**Creating the policy**:   
   
```bash
aws iam create-policy \
--policy-name changePwd \
--policy-document file://changePwdPolicy.json
```
   
   
Copy the ARN of the policy from the output.   
   
**Assigning policy to user group**:   
   
```bash
aws iam attach-group-policy \
--group-name MyGroupCli \
--policy-arn <copied-policy-arn>
```
   
   
## Create Access keys   
   
**For new User**   
   
```bash
aws iam create-access-key --user-name MyUserCli
```
   
   
Copy the `AccessKeyId` and `SecretAccessKey` from the output in order to login as that user from the Cli (programmatic access).   
   
## Switch User   
   
**In the Cli**   
   
There are 3 ways of switching the user in the Cli:   
   
1. `aws configure` to overwrite `~/.aws/` which was set previously.   
2. Use `aws configure set` to overwrite only the credentials.   
   
   - `aws configure set aws_access_key_id <access-key>`   
3. Set bash [environment variable](../devlog/environment%20variable.md)s to temporarily switch a user. It will automatically use the new credentials in that session(terminal).   
   
   - `export AWS_ACCESS_KEY_ID=<access-key>`   
   - `export AWS_SECRET_ACCESS_KEY=<secret-key>`   
   - Optionally you can also change your default region using `AWS_DEFAULT_REGION`   
   
## Delete Resources   
   
`aws ec2 delete-` commands to delete your EC2 resources.   
   
## Profiles   
   
A named profile is a collection of settings and credentials that you can apply to a AWS CLI command. When you specify a profile to run a command, the settings and credentials are used to run that command. Multiple named profiles can be stored in the config and credentials files.   
   
See also: [terraform](../devlog/terraform.md) :)   
   
## Examples   
   
```bash
aws ec2 describe-instances --query "Reservations[].Instances[].{InstanceId:InstanceId,PublicIP:PublicIpAddress,PrivateIP:PrivateIpAddress,Location:Placement.AvailabilityZone,Name:Tags[?Key=='Name']|[0].Value,Type:InstanceType,Status:State.Name,VpcId:VpcId, MAC:NetworkInterfaces[0].MacAddress, OS:PlatformDetails,DNS:PrivateDnsName}" --filters Name=instance-state-name,Values=running --output table
```
   
   
The `aws ec2 describe-instances` command is used to list information about Amazon Elastic Compute Cloud (EC2) instances.   
   
The `--query` option allows you to specify a JMESPath query to filter the results. The query provided in the example will return the following information for each instance:   
   
   
-   `InstanceId`: the ID of the instance   
-   `PublicIP`: the public IP address of the instance   
-   `PrivateIP`: the private IP address of the instance   
-   `Location`: the availability zone in which the instance is located   
-   `Name`: the name of the instance (as specified by the 'Name' tag)   
-   `Type`: the type of instance (e.g. t2.micro)   
-   `Status`: the current status of the instance (e.g. running)   
-   `VpcId`: the ID of the virtual private cloud (VPC) in which the instance is located   
-   `MAC`: the MAC address of the instance   
-   `OS`: the operating system of the instance   
-   `DNS`: the private DNS name of the instance   
   
The `--filters` option is used to filter the results based on the specified criteria. In this case, the command will only return instances with a `Name` of `instance-state-name` and a `Values` of `running`.   
   
The `--output` option allows you to specify the format in which the results should be output. In this case, the results will be output in a table format.   
   
## Resources   
   
   
- [aws — AWS CLI 2.8.0 Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html)
   
   
## Resources   
   
   
- [JB4GDI/awsfaviconupdater: IAM shouldn't be the only tab with a unique favicon! This Chrome Extension sets favicons for many AWS services, so your tabs make more sense.](https://github.com/JB4GDI/awsfaviconupdater)   
- [iann0036/AWSConsoleRecorder: Records actions made in the AWS Management Console and outputs the equivalent CLI/SDK commands and CloudFormation/Terraform templates.](https://github.com/iann0036/AWSConsoleRecorder)   
- [The Cloud Developer Workbook](https://workbook.ryanlewis.dev/)