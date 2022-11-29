---
created: 1664803517448
desc: ''
id: sr12czxr3m1v55n7w3qehg8
title: Flashcards
updated: 1664804112681
---
   
## Explain the following   
   
   
- Availability zone   
- Region   
- Edge location   
   
AWS regions are data centers hosted across different geographical locations worldwide.<br>   
   
Within each region, there are multiple isolated locations known as Availability Zones. Each availability zone is one or more data-centers with redundant network and connectivity and power supply. Multiple availability zones ensure high availability in case one of them goes down.<br>   
   
Edge locations are basically content delivery network which caches data and insures lower latency and faster delivery to the users in any location. They are located in major cities in the world.   
   
## True or False? Each AWS region is designed to be completely isolated from the other AWS regions   
   
True.   
   
## True or False? Each region has a minimum number of 1 availability zones and the maximum is 4   
   
False. The minimum is 2 while the maximum is 6.   
   
## What considerations to take when choosing an AWS region for running a new application?   
   
   
- Services Availability: not all service (and all their features) are available in every region   
- Reduced latency: deploy application in a region that is close to customers   
- Compliance: some countries have more strict rules and requirements such as making sure the data stays within the borders of the country or the region. In that case, only specific region can be used for running the application   
- Pricing: the pricing might not be consistent across regions so, the price for the same service in different regions might be different.   
   
### IAM   
   
## What is IAM? What are some of its features?   
   
In short, it's used for managing users, groups, access policies & roles   
Full explanation can be found [here](https://aws.amazon.com/iam)   
   
## True or False? IAM configuration is defined globally and not per region   
   
True   
   
## True or False? When creating an AWS account, root account is created by default. This is the recommended account to use and share in your organization   
   
False. Instead of using the root account, you should be creating users and use them.   
   
## True or False? Groups in AWS IAM, can contain only users and not other groups   
   
True   
   
## True or False? Users in AWS IAM, can belong only to a single group   
   
False. Users can belong to multiple groups.   
   
## What are some best practices regarding IAM in AWS?   
   
   
- Delete root account access keys and don't use root account regularly   
- Create IAM user for any physical user. Don't share users.   
- Apply "least privilege principle": give users only the permissions they need, nothing more than that.   
- Set up MFA and consider enforcing using it   
- Make use of groups to assign permissions ( user -> group -> permissions )   
   
## What permissions does a new user have?   
   
Only a login access.   
   
## True or False? If a user in AWS is using password for authenticating, he doesn't needs to enable MFA   
   
False(!). MFA is a great additional security layer to use for authentication.   
   
## What ways are there to access AWS?   
   
   
- AWS Management Console   
- AWS CLI   
- AWS SDK   
   
## What are Roles?   
   
[AWS docs](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html): "An IAM role is an IAM identity that you can create in your account that has specific permissions...it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS."   
For example, you can make use of a role which allows EC2 service to access s3 buckets (read and write).   
   
## What are Policies?   
   
Policies documents used to give permissions as to what a user, group or role are able to do. Their format is JSON.   
   
## A user is unable to access an s3 bucket. What might be the problem?   
   
There can be several reasons for that. One of them is lack of policy. To solve that, the admin has to attach the user with a policy what allows him to access the s3 bucket.   
   
## What should you use to:   
   
   
- Grant access between two services/resources?   
- Grant user access to resources/services?   
   
* Role   
* Policy   
   
## What statements AWS IAM policies are consist of?   
   
   
- Sid: identifier of the statement (optional)   
- Effect: allow or deny access   
- Action: list of actions (to deny or allow)   
- Resource: a list of resources to which the actions are applied   
- Principal: role or account or user to which to apply the policy   
- Condition: conditions to determine when the policy is applied (optional)   
   
## Explain the following policy:   
   
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect:": "Allow",
            "Action": "*",
            "Resources": "*"
        }
    ]
}
```
   
   
This policy permits to perform any action on any resource. It happens to be the "AdministratorAccess" policy.   
   
## What security tools AWS IAM provides?   
   
   
- IAM Credentials Report: lists all the account users and the status of their credentials   
- IAM Access Advisor: Shows service permissions granted to a user and information on when he accessed these services the last time   
   
## Which tool would you use to optimize user permissions by identifying which services he doesn't regularly (or at all) access?   
   
IAM Access Advisor   
   
## What type of IAM object would you use to allow inter-service communication?   
   
Role   
   
### EC2   
   
## What is EC2?   
   
"a web service that provides secure, resizable compute capacity in the cloud".   
Read more [here](https://aws.amazon.com/ec2)   
   
## True or False? EC2 is a regional service   
   
True. As opposed to IAM for example, which is a global service, EC2 is a regional service.   
   
## What are some of the properties/configuration options of EC2 instances that can be set or modified?   
   
   
- OS (Linux, Windows)   
- RAM and CPU   
- Networking - IP, Card properties like speed   
- Storage Space - (EBS, EFS, EC2 Instance Store)   
- EC2 User Data   
- Security groups   
   
## What would you use for customizing EC2 instances? As in software installation, OS configuration, etc.   
   
AMI. With AMI (Amazon Machine Image) you can customize EC2 instances by specifying which software to install, what OS changes should be applied, etc.   
   
#### AMI   
   
## What is AMI?   
   
Amazon Machine Images is "An Amazon Machine Image (AMI) provides the information required to launch an instance".   
Read more [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)   
   
## What are the different sources for AMIs?   
   
   
- Personal AMIs - AMIs you create   
- AWS Marketplace for AMIs - AMIs made by others, mostly sold for some price   
- Public AMIs - Provided by AWS   
   
## True or False? AMI are built for specific region   
   
True (but they can be copied from one region to another).   
   
## Describe in high-level the process of creating AMIs   
   
1. Start an EC2 instance   
2. Customized the EC2 instance (install packages, change OS configuration, etc.)   
3. Stop the instance (for avoiding data integrity issues)   
4. Create EBS snapshot and build an AMI   
5. To verify and test the AMI, launch an instance from the AMI   
   
## What is an instance type?   
   
"the instance type that you specify determines the hardware of the host computer used for your instance"   
Read more about instance types [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html)   
   
## Explain the instance type naming convention   
   
Let's take for example the following instance type: m5.large   
   
`m` is the instance class   
`5` is the generation   
`large` is the size of the instance (affects the spec properties like vCPUs and RAM)   
   
## True or False? The following are instance types available for a user in AWS:   
   
   
- Compute optimized   
- Network optimized   
- Web optimized   
   
False. From the above list only compute optimized is available.   
   
## Explain each of the following instance types:   
   
   
- "Compute Optimized"   
- "Memory Optimized"   
- "Storage Optimized"   
   
Compute Optimized:   
   
   
- Used for compute-intensive tasks   
- It has high performance processors   
- Use cases vary: gaming serves, machine learning, batch processing, etc.   
   
Memory Optimized:   
   
   
- Used for processing large data sets in memory   
- Other use cases: high performance, databases, distributed cache stores   
   
Storage Optimized:   
   
   
- Used for storage intensive tasks - high read and write access to large data sets   
- Use cases: databases, OLTP system, distributing file systems   
   
## What can you attach to an EC2 instance in order to store data?   
   
EBS   
   
#### EBS   
   
## Explain Amazon EBS   
   
[AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html): "provides block level storage volumes for use with EC2 instances. EBS volumes behave like raw, unformatted block devices."   
   
## What happens to EBS volumes when the instance is terminated?   
   
By deafult, the root volume is marked for deletion, while other volumes will still remain.<br>   
You can control what will happen to every volume upon termination.   
   
## What happens to the EC2 disk (EBS) when the instance is stopped?   
   
Disk is intact and can be used when the instance starts.   
   
## True or False? EBS volumes are locked to a specific availability zone   
   
True   
   
## Explain EBS Snapshots   
   
EBS snapshots used for making a backup of the EBS volume at point of time.   
   
## What are the use cases for using EBS snapshots?   
   
   
- Backups of the data   
- Moving the data between AZs   
   
## Is it possible to attach the same EBS volume to multiple EC2 instances?   
   
Yes, with multi-attach it's possible to attach a single EBS volume to multiple instances.   
   
## True or False? EBS is a network drive hence, it requires network connectivity   
   
True   
   
## What EBS volume types are there?   
   
   
- HDD (st 1, sc 1): Low cost HDD volumes   
- SSD   
  - io1, io2: Highest performance SSD   
  - gp2, gp3: General purpose SSD   
   
## If you need an EBS volume for low latency workloads, which volume type would you use?   
   
SSD - io1, io2   
   
## If you need an EBS volume for workloads that require good performance but the cost is also an important aspect for you, which volume type would you use?   
   
SSD - gp2, gp3   
   
## If you need an EBS volume for high-throughput, which volume type would you use?   
   
SSD - io1, io2   
   
## If you need an EBS volume for infrequently data access, which volume type would you use?   
   
HDD - sc1   
   
## Which EBS volume types can be used as boot volumes for EC2 instances?   
   
SSD: gp2, gp3, io1, io2   
   
## True or False? In EBS gp2 volume type, IP will increase if the disk size increases   
   
True.   
   
#### Instance Store   
   
## If you would like to have an hardware disk attached to your EC2 instead of a network one (EBS). What would you use?   
   
EC2 Instance Store.   
   
## Explain EC2 Instance Store. Why would someone choose to use it over other options?   
   
EC2 instance store provides better I/O performances when compared to EBS.<br>   
It is mostly used for cache and temporary data purposes.   
   
## Are there any disadvantages in using instance store over EBS?   
   
Yes, the data on instance store is lost when they are stopped.   
   
#### EFS   
   
## What is Amazon EFS?   
   
[AWS Docs](https://aws.amazon.com/efs): "Amazon Elastic File System (Amazon EFS) provides a simple, scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources."   
   
In simpler words, it's a network file system you can mount on one or more EC2 instances.   
   
## True or False? EFS is locked into a single availability zone   
   
False. EFS can be mounted across multiple availability zones.   
   
## What are some use cases for using EFS?   
   
   
- Data sharing (e.g. developers working on the same source control)   
- Web serving   
- Content management   
   
## True or False? EFS only compatible with Linux based AMI   
   
True   
   
## True or False? EFS requires the user to perform capacity planning as it doesn't scales automatically   
   
False. EFS scales automatically and you pay-per-use.   
   
## What EFS modes are there?   
   
   
- Performance mode   
  - General purpose: used mainly for CMS, web serving, ... as it's optimal for latency sensitive applications   
  - Max I/O: great for scaling to high levels of throughput and I/O operations per second   
- Throughput mode   
  - Bursting: scale throughput based on FS size   
  - Provisioned: fixed throughput   
   
## Which EFS mode would you use if you need to perform media processing?   
   
Performance Mode (Max I/O): It provides high throughput and scales to operations per second. Mainly used for big data, media processing, etc.   
   
## What is the default EFS mode?   
   
Performance Mode (General Purpose): Used for web serving, CMS, ... anything that is sensitive to latency.   
   
## What EFS storage tiers are there?   
   
   
- Standard: frequently accessed files   
- Infrequent access: lower prices to store files but it also costs to retrieve them   
   
#### Pricing Models   
   
## What EC2 pricing models are there?   
   
On Demand - pay a fixed rate by the hour/second with no commitment. You can provision and terminate it at any given time.   
Reserved - you get capacity reservation, basically purchase an instance for a fixed time of period. The longer, the cheaper.   
Spot - Enables you to bid whatever price you want for instances or pay the spot price.   
Dedicated Hosts - physical EC2 server dedicated for your use.   
   
## True or False? Reserved instance has to be used for a minimum of 1 year   
   
True.   
   
## Explain the following types of reserved instances:   
   
   
- Convertible Reserved Instances   
- Scheduled Reserved Instances   
   
   
- Convertible Reserved Instances: used for long running workloads but used when instance type might change during the period of time it's reserved   
- Scheduled Reserved Instances: when you need to reserve an instance for a long period but you don't need it continuously (so for example you need it only in the morning)   
   
## True or False? In EC2 On Demand, you pay per hour when using Linux or Windows and per second (after first minute) when using any other operating system   
   
False. You pay per second (after the first minute) when using Windows or Linux and per hour for any other OS.   
   
## You need an instance for short-term and the workload running on instance must not be interrupted. Which pricing model would you use?   
   
On Demand is good for short-term non-interrupted workloads (but it also has the highest cost).   
   
## You need an instance for running an application for a period of 2 years continuously, without changing instance type. Which pricing model would you use?   
   
Reserved instances: they are cheaper than on-demand and the instance is yours for the chosen period of time.   
   
## Which pricing model has potentially the biggest discount and what its advantage   
   
Spot instances provide the biggest discount but has the disadvantage of risking losing them due bigger bid price.   
   
## You need an instance for two years, but only between 10:00-15:00 every day. Which pricing model would you use?   
   
Reserved instances from the "Scheduled Reserved Instances" type which allows you to reserve for specific time window (like 10:00-15:00 every day).   
   
## You need an instance for running workloads. You don't care if they fail for a given moment as long as they run eventually. Which pricing model would you use?   
   
Spot instances. The discount potential is the highest compared to all other pricing models. The disadvantage is that you can lose the instance at any point so, you must run only workloads that you are fine with them failing suddenly.   
   
## You need a physical server only for your use. Which pricing model are you going to use?   
   
EC2 Dedicated Host   
   
## What are some of the differences between dedicated hosts and dedicated instances?   
   
In dedicated hosts you have per host billing, you have more visibility (sockets, cores, ...) and you can control where instance will be placed.<br>   
In dedicated instances the billing is per instance but you can't control placement and you don't have visibility of sockets, cores, ...   
   
## For what use cases, EC2 dedicated hosts are useful for?   
   
   
- Compliance needs   
- When the software license is complex (Bring Your Own License) and doesn't support cloud or multi-tenants   
- Regulatory requirements   
   
## What are Security Groups?   
   
"A security group acts as a virtual firewall that controls the traffic for one or more instances"   
More on this subject [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)   
   
## True or False? Security groups only contain deny rules   
   
False. Security groups only contain allow rules.   
   
## True or False? One security group can be attached to multiple instances   
   
True   
   
## True or False? Security groups are not locked down to a region and VPC (meaning you don't have to create a new one when switching regions)   
   
False. They are locked down to regions and VPC.   
   
## True or False? By default, when using security groups, all inbound traffic to an EC2 instance is blocked and all outbound traffic is allowed   
   
True   
   
## What is the advantage of referencing security groups from a given security group?   
   
Imagine you have an instance referencing two security groups, allowing to get inbound traffic from them.<br>   
Now imagine you have two instances, each using one of the security groups referenced in the instance we've just mentioned. This means you can get traffic from these two instances because they use security groups which referenced in the instance mentioned at the beginning. No need to use IPs.   
   
## How to migrate an instance to another availability zone?   
   
## What can you attach to an EC2 instance in order to store data?   
   
EBS   
   
## What EC2 reserved instance types are there?   
   
Standard RI - most significant discount + suited for steady-state usage   
Convertible RI - discount + change attribute of RI + suited for steady-state usage   
Scheduled RI - launch within time windows you reserve   
   
Learn more about EC2 RI [here](https://aws.amazon.com/ec2/pricing/reserved-instances)   
   
## For how long can reserved instances be reserved?   
   
1 or 3 years.   
   
## What allows you to control inbound and outbound instance traffic?   
   
Security Groups   
   
## What bootstrapping means and how to use it in AWS EC2?   
   
Bootstrapping is about launching commands when a machine starts for the first time.   
In AWS EC2 this is done using the EC2 user data script.   
   
## You get time out when trying reach your application which runs on an EC2 instance. Specify one reason why it would possibly happen   
   
Security group isn't configured properly.   
   
## What is the AWS Instance Connect?   
   
[AWS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Connect-using-EC2-Instance-Connect.html): "Amazon EC2 Instance Connect provides a simple and secure way to connect to your Linux instances using Secure Shell (SSH)."   
   
## You try to run EC2 commands in an EC2 instance you've just created but it fails due to missing credentials. What would you do?   
   
DO NOT configure AWS credentials on the instance (this means anyone else in your account would be able to use and see your credentials).<br>   
The best practice is to attach an IAM role with sufficient permissions (like `IAMReadOnlyAccess`)   
   
## True or False? Cancelling a Spot instance request terminates the instance   
   
False. When you cancel a Spot instance request, you are not terminating the instances created by it.<br>   
To terminate such instances, you must cancel the Spot instance request first.   
   
## What are Spot Fleets?   
   
Set of Spot instances and if you would like, also on-demand instances.   
   
## What strategies are there to allocate Spot instances?   
   
   
- lowestPrice: launch instances from the pool that has the lowest price   
- diversified: distributed across all pools   
- capacityOptimized: optimized based on the number of instances   
   
## From networking perspective, what do you get by default when running an EC2 instance?   
   
A private IP and a public IP.   
   
## Explain EC2 hibernate   
   
[AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Hibernate.html: "Hibernation saves the contents from the instance memory (RAM) to your Amazon Elastic Block Store (Amazon EBS) root volume."   
   
## True or False? Using EC2 hibernate option results in having faster instance boot   
   
True. This is because the operating system isn't restarted or stopped.   
   
## What are some use cases for using EC2 hibernate option?   
   
   
- Save RAM state   
- Service with long time initialization   
- Keep long-running processes   
   
## What are some limitations of EC2 hibernate option?   
   
   
- Instance RAM size is limited   
- Root volume must be encrypted EBS   
- Hibernation time is limited   
- Doesn't supports all instances types   
- No support for bare metal. Only On-Demand and Reserved instances   
- Doesn't supports all AMIs   
   
## Explain what is EC2 Nitro   
   
   
- Next generation EC2 instances using new virtualization technology   
- Better EBS: 64,000 EBS IOPS   
- Better networking: HPC, IPv6   
- Better security   
   
## What CPU customization is available with EC2?   
   
   
- Modifying number of CPU cores (useful for high RAM and low CPU applications)   
- Modifying number of threads per cure (useful for HPC workloads)   
   
## Explain EC2 Capacity Reservations   
   
   
- Allows you to ensure you have EC2 capacity when you need it   
- Usually combined with Reserved Instances and Saving Plans to achieve cost saving   
   
#### Launch Template   
   
## What is a launch template?   
   
[AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-templates.html): "You can create a launch template that contains the configuration information to launch an instance. You can use launch templates to store launch parameters so that you do not have to specify them every time you launch an instance"   
   
## What is the difference between Launch Configuration and Launch Template?   
   
Launch configuration is a legacy form of Launch Template that must be recreated every time you would like to update the configuration.   
   
In addition, launch template has the clear benefits of:   
   
   
- Provision both On-Demand and Spot instances   
- supporting multiple versions   
- support creating parameters subsets (used for re-use and inheritance)   
   
#### ENI   
   
## Explain Elastic Network Interfaces (ENI)   
   
[AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html): "An elastic network interface is a logical networking component in a VPC that represents a virtual network card."   
   
## Name at least three attributes the Elastic Network Interfaces (ENI) can include   
   
1. One public IPv4 address   
2. Mac Address   
3. A primary private IPv4 address (from the address range of your VPC)   
   
## True or False? ENI are not bound to a specific availability zone   
   
False. ENI are bound to specific availability zone.   
   
## True or False? ENI can be created independently of EC2 instances   
   
True. They can be attached later on and on the fly (for failover purposes).   
   
#### Placement Groups   
   
## What are "Placement Groups"?   
   
[AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html): "When you launch a new EC2 instance, the EC2 service attempts to place the instance in such a way that all of your instances are spread out across underlying hardware to minimize correlated failures. You can use placement groups to influence the placement of a group of interdependent instances to meet the needs of your workload."   
   
## What Placement Groups strategies are there?   
   
   
- Cluster: places instance close together in an AZ.   
- Spread: spreads the instance across the hardware   
- Partition: spreads the instances across different partitions (= different sets of hardware/racks) within an AZ   
   
## For each of the following scenarios choose a placement group strategy:   
   
   
- High availability is top priority   
- Low latency between instances   
- Instances must be isolated from each other   
- Big Data applications that are partition aware   
- Big Data process that needs to end quickly   
   
   
- High availability is top priority - Spread   
- Low latency between instances - Cluster   
- Instances must be isolated from each other - Spread   
- Big Data applications that are partition aware - Partition   
- Big Data process that needs to end quickly - Cluster   
   
## What are the cons and pros of the "Cluster" placement group strategy?   
   
Cons: if the hardware fails, all instances fail   
Pros: Low latency & high throughput network   
   
## What are the cons and pros of the "Spread" placement group strategy?   
   
Cons:   
   
   
- Current limitation is 7 instances per AZ (per replacement group)   
  Pros:   
   
- Maximized high availability (instances on different hardware, span across AZs)   
   
### VPC   
   
## What is VPC?   
   
"A logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define"   
Read more about it [here](https://aws.amazon.com/vpc).   
   
## True or False? VPC spans multiple regions   
   
False   
   
## True or False? It's possible to have multiple VPCs in one region   
   
True. As of today, the soft limit is 5.   
   
## True or False? Subnets belong to the same VPC, can be in different availability zones   
   
True. Just to clarify, a single subnet resides entirely in one AZ.   
   
## You have noticed your VPC's subnets (which use x.x.x.x/20 CIDR) have 4096 available IP addresses although this CIDR should have 4096 addresses. What is the reason for that?   
   
AWS reserves 5 IP addresses in each subnet - first 4 and the last one, and so they aren't available for use.   
   
## What AWS uses the 5 reserved IP addresses for?   
   
x.x.x.0 - network address   
x.x.x.1 - VPC router   
x.x.x.2 - DNS mapping   
x.x.x.3 - future use   
x.x.x.255 - broadcast address   
   
## What is an Internet Gateway?   
   
[AWS Docs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html): "component that allows communication between instances in your VPC and the internet"   
   
In addition it's good to know that IGW is:   
   
   
- Highly available and redundant   
- Not porivding internet access by its own (you need route tables to be edited)   
- Created separately from VPC   
   
## True or False? One or more VPCs can be attached to one Internet Gateway   
   
False. Only one VPC can be attached to one IGW and vice versa   
   
## True or False? NACL allow or deny traffic on the subnet level   
   
True   
   
## What is VPC peering?   
   
[docs.aws](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html): "A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses."   
   
## True or False? Multiple Internet Gateways can be attached to one VPC   
   
False. Only one internet gateway can be attached to a single VPC.   
   
## You've restarted your EC2 instance and the public IP has changed. How would you deal with it so it won't happen?   
   
Use Elastic IP which provides you a fixed IP address.   
   
## When creating a new VPC, there is an option called "Tenancy". What is it used for?   
   
## What is an Elastic IP address?   
   
[AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html): "An Elastic IP address is a static IPv4 address designed for dynamic cloud computing. An Elastic IP address is allocated to your AWS account, and is yours until you release it. By using an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account."   
   
## Why would you use an Elastic IP address?   
   
Let's say you have an instance that you need to shutdown or perform some maintenance on. In that case, what you would want to do is to move the Elastic IP address to another instance that is operational, until you finish to perform the maintenance and then you can move it back to the original instance (or keep it assigned to the second one).   
   
## True or False? When stopping and starting an EC2 instance, its public IP changes   
   
True   
   
## What are the best practices around Elastic IP?   
   
The best practice is actually not using them in the first place. It's more common to use a load balancer without a public IP or use a random public IP and register a DNS record to it   
   
## True or False? An Elastic IP is free, as long it's not associated with an EC2 instance   
   
False. An Elastic IP is free of charge as long as **it is ** associated with an EC2 instance. This instance should be running and should have only one Elastic IP.   
   
## True or False? Route Tables used to allow or deny traffic from the internet to AWS instances   
   
False.   
   
## Explain Security Groups and Network ACLs   
   
   
- NACL - security layer on the subnet level.   
- Security Group - security layer on the instance level.   
   
Read more about it [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html) and [here](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)   
   
## What is AWS Direct Connect?   
   
Allows you to connect your corporate network to AWS network.   
   
## What would you use if you need a fixed public IP for your EC2 instance?   
   
Elastic IP   
   
## Kratos, your colleague, decided to use a subnet of /27 because he needs 29 IP addresses for EC2 instances. Is Kratos right?   
   
No. Since AWS reserves 5 IP addresses for every subnet, Kratos will have 32-5=27 addresses and this is less than what he needs (29).   
   
It's better if Kratos uses a subnet of size /26 but good luck telling him that.   
   
#### Default VPC   
   
## True or False? By default, any new account has a default VPC   
   
True.   
   
## True or False? Default VPC doesn't have internet connectivity and any launched EC2 will only have a private IP assigned   
   
False. The default VPC has internet connectivity and any launched EC2 instance gets a public IPv4 address.   
   
In addition, any launched EC2 instance gets a public and private DNS names.   
   
## Which of the following is included with default VPC?   
   
   
- Internet gateway connected to the default VPC   
- A route to main route table that points all traffic to internet gateway   
- Default public subnet   
- Default /16 IPv4 CIDR block   
   
All of them :)   
   
### Lambda   
   
## Explain what is AWS Lambda   
   
AWS definition: "AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume."   
   
Read more on it [here](https://aws.amazon.com/lambda)   
   
## True or False? In AWS Lambda, you are charged as long as a function exists, regardless of whether it's running or not   
   
False. Charges are being made when the function is executed for the time it takes to execute and compute resources it uses.   
   
## Which of the following set of languages Lambda supports?   
   
   
- R, Swift, Rust, Kotlin   
- Python, Ruby, Go, Kotlin, Bash   
- Python, Ruby, PHP, PowerShell, C#, Perl   
- Python, Ruby, Go, Node.js, Groovy, C++   
- Python, Ruby, Go, Node.js, PowerShell, C#   
   
   
- Python, Ruby, Go, Node.js, PowerShell, C#   
   
## True or False? Basic lambda permissions allow you only to upload logs to Amazon CloudWatch Logs   
   
True   
   
## What's one of the issues with the current architecture?   
   
![](assets/images/2022-10-03-19-00-48.png)   
   
%   
   
Users shouldn't access directly AWS Lambda directly. If you'd to like to expose your Lambda function to users a better approach would be to set up API Gateway endpoint between the users and the Lambda function.   
   
This not only provides enhanced security but also easier access for the user where he can use HTTP or HTTPS for accessing the function.   
   
## Specify one or more use cases for using AWS Lambda   
   
   
- Uploading images to S3 and tagging them or inserting information on the images to a database   
- Uploading videos to S3 and edit them or add subtitles/captions to them and store the result in S3   
- Use SNS and/or SQS to trigger functions based on notifications or messages receieved from these services.   
- Cron Jobs: Use Lambda together with CloudWatch events to schedule tasks/functions periodically.   
   
## You run an architecture where you have a Lambda function that uploads images to S3 bucket and stores information on the images in DynamoDB. You would like to expose the function to users so they can invoke it. Your friend Carlos suggests you expose the credentials to the Lambda function. What's your take on that?   
   
That's a big no. You shouldn't let users direct access to your Lambda function.   
   
The way to go here and expose the Lambda function to users is to to an API Gateway endpoint.   
   
### Containers   
   
#### ECS   
   
## What is Amazon ECS?   
   
[AWS Docs](https://aws.amazon.com/ecs): "Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service. Customers such as Duolingo, Samsung, GE, and Cook Pad use ECS to run their most sensitive and mission critical applications because of its security, reliability, and scalability."   
   
In simpler words, it allows you to launch containers on AWS.<br>   
While AWS takes care of starting/stopping containers, you need to provision and maintain the infrastructure where the containers are running (EC2 instances).   
   
## What one should do in order to make EC2 instance part of an ECS cluster?   
   
Install ECS agent on it. Some AMIs have built-in configuration for that.   
   
## What ECS launch types are there?   
   
   
- EC2 Instance   
- AWS Fargate   
   
## What is Amazon ECR?   
   
[AWS Docs](https://aws.amazon.com/ecr): "Amazon Elastic Container Registry (ECR) is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images."   
   
## What the role "EC2 Instance Profile" is used for in regards to ECS?   
   
EC2 Instance Profile used by ECS agent on an EC2 instance to:   
   
   
- Make API calls to ECS Service   
- Send logs to CloudWatch from the container   
- Use secrets defined in SSM Parameter Store or Secrets Manager   
- Pull container images from ECR (Registry)   
   
## How to share data between containers (some from ECS and some from Fargate)?   
   
Using EFS is a good way to share data between containers and it works also between different AZs.   
   
#### Fargate   
   
## What is AWS Fargate?   
   
[Amazon Docs](https://aws.amazon.com/fargate): "AWS Fargate is a serverless, pay-as-you-go compute engine that lets you focus on building applications without managing servers. AWS Fargate is compatible with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS)"   
   
In simpler words, AWS Fargate allows you launch containers on AWS without worrying about managing infrastructure. It runs containers based on the CPU and RAM you need.   
   
## How AWS Fargate different from AWS ECS?   
   
In AWS ECS, you manage the infrastructure - you need to provision and configure the EC2 instances.<br>   
While in AWS Fargate, you don't provision or manage the infrastructure, you simply focus on launching Docker containers. You can think of it as the serverless version of AWS ECS.   
   
## True or False? Fargate creates an ENI for every task it runs   
   
True.   
   
### S3   
   
#### Basics   
   
## Explain what is AWS S3?   
   
   
- S3 is a object storage service which is fast, scalable and durable. S3 enables customers to upload, download or store any file or object that is up to 5 TB in size.<br>   
- S3 stands for: Simple Storage Service   
- As a user you don't have to worry about filesystems or disk space   
   
#### Buckets 101   
   
## What is a bucket?   
   
An S3 bucket is a resource which is similar to folders in a file system and allows storing objects, which consist of data.   
   
## True or False? Buckets are defined globally   
   
False. They are defined at the region level.   
   
## True or False? A bucket name must be globally unique   
   
True   
   
## How to rename a bucket in S3?   
   
A S3 bucket name is immutable. That means it's not possible to change it, without removing and creating a new bucket.   
   
This is why the process for renaming a bucket is as follows:   
   
   
- Create a new bucket with the desired name   
- Move the data from the old bucket to it   
- Delete the old bucket   
   
With the AWS CLI that would be:   
   
```sh
# Create new bucket
aws s3 mb s3://[NEW_BUCKET_NAME]
# Sync the content from the old bucket to the new bucket
$ aws s3 sync s3://[OLD_BUCKET_NAME] s3://[NEW_BUCKET_NAME]
# Remove old bucket
$ aws s3 rb --force s3://[OLD_BUCKET_NAME]
```
   
   
## True or False? The max object size a user can upload in one go, is 5TB   
   
True   
   
## Explain "Multi-part upload"   
   
[Amazon docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html): "Multipart upload allows you to upload a single object as a set of parts. Each part is a contiguous portion of the object's data...In general, when your object size reaches 100 MB, you should consider using multipart uploads instead of uploading the object in a single operation."   
   
#### Objects   
   
## Explain "Object Versioning"   
   
When enabled at a bucket level, versioning allows you to upload new version of files, overriding previous version and so be able to easily roll-back and protect your data from being permanently deleted.   
   
## Explain the following:   
   
   
- Object Lifecycles   
- Object Sharing   
   
* Object Lifecycles - Transfer objects between storage classes based on defined rules of time periods   
* Object Sharing - Share objects via a URL link   
   
## Explain Object Durability and Object Availability   
   
Object Durability: The percent over a one-year time period that a file will not be lost   
Object Availability: The percent over a one-year time period that a file will be accessible   
   
#### S3 Security   
   
## True or False? Every new S3 bucket is public by default   
   
False. A newly created bucket is private unless it was configured to be public.   
   
## What's a presigned URL?   
   
Since every newly created bucket is by default private it doesn't allows to share files with users. Even if the person who uploaded them tries to view them, it gets denied.   
   
A presigned URL is a way to bypass that and allow sharing the files with users by including the credentials (token) as part of the URL. It can be done for limited time.   
   
## What security measures have you taken in context of S3?   
   
    * Don't make a bucket public.   
    * Enable encryption if it's disabled.   
    * Define an access policy   
   
## What encryption types supported by S3?   
   
   
- SSE-S3   
- SSE-KMS   
- SSE-C   
   
## Describe shortly how SSE-S3 (AES) encryption works   
   
1. You upload a file to S3 using HTTP (or HTTPS) and header   
2. S3 uses the managed data key to encrypt it   
3. S3 stores the encrypted object in the bucket   
   
## True or False? In case of SSE-S3 (AES-256) encryption, you manage the key   
   
False. S3 manages the key and uses AES-256 algorithm for the encryption.   
   
## Who or what manages the keys in the case of SSE-KMS encryption?   
   
The KMS service.   
   
## Why would someone choose to use SSE-KMS instead of SSE-S3?   
   
SS3-KMS provides control over who has access to the keys and you can also enabled audit trail.   
   
## True or False? In case of SSE-C encryption, both S3 and you manage the keys   
   
False. You manage the keys. It's customer provided keys.   
   
## True or False? In case of SSE-C HTTPS must be used and encryption key must be provided in headers for every HTTP request   
   
True.   
   
## Describe shortly how SSE-C encryption works   
   
1. User uploads a file to S3 using HTTPS while providing data key in the header   
2. AWS S3 performs the encryption using the provided data key and encrypted object is stored in the bucket   
   
If a user would like to get the object, the same data key would have to be provided.   
   
## With which string an header starts?   
   
   
- x-zmz   
- x-amz   
- x-ama   
   
x-amz   
   
#### Misc   
   
## What is a storage class? What storage classes are there?   
   
Each object has a storage class assigned to, affecting its availability and durability. This also has effect on costs.   
Storage classes offered today:   
   
   
- Standard:   
   
   
  - Used for general, all-purpose storage (mostly storage that needs to be accessed frequently)   
  - The most expensive storage class   
  - 11x9% durability   
  - 2x9% availability   
  - Default storage class   
   
   
- Standard-IA (Infrequent Access)   
   
   
  - Long lived, infrequently accessed data but must be available the moment it's being accessed   
  - 11x9% durability   
  - 99.90% availability   
   
   
- One Zone-IA (Infrequent Access):   
   
   
  - Long-lived, infrequently accessed, non-critical data   
  - Less expensive than Standard and Standard-IA storage classes   
  - 2x9% durability   
  - 99.50% availability   
   
   
- Intelligent-Tiering:   
   
   
  - Long-lived data with changing or unknown access patterns. Basically, In this class the data automatically moves to the class most suitable for you based on usage patterns   
  - Price depends on the used class   
  - 11x9% durability   
  - 99.90% availability   
   
   
- Glacier: Archive data with retrieval time ranging from minutes to hours   
- Glacier Deep Archive: Archive data that rarely, if ever, needs to be accessed with retrieval times in hours   
- Both Glacier and Glacier Deep Archive are:   
  - The most cheap storage classes   
  - have 9x9% durability   
   
More on storage classes [here](https://aws.amazon.com/s3/storage-classes)   
   
## A customer would like to move data which is rarely accessed from standard storage class to the most cheapest class there is. Which storage class should be used?   
   
   
- One Zone-IA   
- Glacier Deep Archive   
- Intelligent-Tiering   
   
Glacier Deep Archive   
   
## What Glacier retrieval options are available for the user?   
   
Expedited, Standard and Bulk   
   
## True or False? Each AWS account can store up to 500 PetaByte of data. Any additional storage will cost double   
   
False. Unlimited capacity.   
   
## Explain what is Storage Gateway   
   
"AWS Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage".   
More on Storage Gateway [here](https://aws.amazon.com/storagegateway)   
   
## Explain the following Storage Gateway deployments types   
   
   
- File Gateway   
- Volume Gateway   
- Tape Gateway   
   
Explained in detail [here](https://aws.amazon.com/storagegateway/faqs)   
   
## What is the difference between stored volumes and cached volumes?   
   
Stored Volumes - Data is located at customer's data center and periodically backed up to AWS   
Cached Volumes - Data is stored in AWS cloud and cached at customer's data center for quick access   
   
## What is "Amazon S3 Transfer Acceleration"?   
   
AWS definition: "Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket"   
   
Learn more [here](https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html)   
   
## Explain data consistency   
   
    S3 Data Consistency provides strong read-after-write consistency for PUT and DELETE requests of objects in the S3 bucket in all AWS Regions. S3 always return latest file version.   
   
## Can you host dynamic websites on S3? What about static websites?   
   
    No. S3 support only statis hosts. On a static website, individual webpages include static content. They might also contain client-side scripts. By contrast, a dynamic website relies on server-side processing, including server-side scripts such as PHP, JSP, or ASP.NET. Amazon S3 does not support server-side scripting.   
   
### Disaster Recovery   
   
## In regards to disaster recovery, what is RTO and RPO?   
   
RTO - The maximum acceptable length of time that your application can be offline.   
   
RPO - The maximum acceptable length of time during which data might be lost from your application due to an incident.   
   
## What types of disaster recovery techniques AWS supports?   
   
   
- The Cold Method - Periodically backups and sending the backups off-site<br>   
- Pilot Light - Data is mirrored to an environment which is always running   
- Warm Standby - Running scaled down version of production environment   
- Multi-site - Duplicated environment that is always running   
   
## Which disaster recovery option has the highest downtime and which has the lowest?   
   
Lowest - Multi-site   
Highest - The cold method   
   
### CloudFront   
   
## Explain what is CloudFront   
   
AWS definition: "Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment."   
   
More on CloudFront [here](https://aws.amazon.com/cloudfront)   
   
## Explain the following   
   
   
- Origin   
- Edge location   
- Distribution   
   
## What delivery methods available for the user with CDN?   
   
## True or False?. Objects are cached for the life of TTL   
   
True   
   
## What is AWS Snowball?   
   
A transport solution which was designed for transferring large amounts of data (petabyte-scale) into and out the AWS cloud.   
   
### ELB   
   
## What is ELB (Elastic Load Balancing)?   
   
[AWS Docs](https://aws.amazon.com/elasticloadbalancing): "Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions."   
   
## True or False? Elastic Load Balancer is a managed resource (= AWS takes care of it)   
   
True. AWS responsible for making sure ELB is operational and takes care of lifecycle operations like upgrades, maintenance and high availability.   
   
## What types of AWS load balancers are there?   
   
   
- Classic Load Balancer (CLB): Mainly for TCP (layer 4) and HTTP, HTTPS (layer 7)   
- Application Load Balancer (ALB): Mainly for HTTP, HTTPS and WebSocket   
- Network Load Balancer (NLB): Mainly for TCP, TLS and UDP   
- Gateway Load Balancer (GWLB): Mainly for layer 3 operations (IP protocol)   
   
## What's a "listener" in regards to ELB?   
   
## What's a "target group" in regards to ELB?   
   
## Which load balancer would you use for services which use HTTP or HTTPS traffic?   
   
Application Load Balancer (ALB).   
   
## What are some use cases for using Gateway Load Balancer?   
   
   
- Intrusion Detection   
- Firewall   
- Payload manipulation   
   
## Explain "health checks" in the context of AWS ELB   
   
Health checks used by ELB to check whether EC2 instance(s) are properly working.<br>   
If health checks fail, ELB knows to not forward traffic to that specific EC2 instance where the health checks failed.   
   
## True or False? AWS ELB health checks are done on a port and a route   
   
True.   
   
For example, port `2017` and endpoint `/health`.   
   
## What types of load balancers are supported in EC2 and what are they used for?   
   
   
- Application LB - layer 7 traffic<br>   
- Network LB - ultra-high performances or static IP address (layer 4)<br>   
- Classic LB - low costs, good for test or dev environments (retired by August 15, 2022)<br>   
- Gateway LB - transparent network gateway and and distributes traffic such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. (layer 3)<br>   
   
## Which type of AWS load balancer is used in the following drawing?   
   
![](assets/images/2022-10-03-19-04-49.png)   
   
Application Load Balancer (routing based on different endpoints + HTTP is used).   
   
## What are possible target groups for ALB (Application Load Balancer)?   
   
   
- EC2 tasks   
- ECS instances   
- Lambda functions   
- Private IP Addresses   
   
## True or False? ALB can route only to a single route group   
   
False. ALB can route to multiple target groups.   
   
## If you wanted to analyze network traffic, you would use the `____ load balancer`   
   
Gateway Load Balancer   
   
## Who has better latency? Application Load Balancer or Network Load Balancer?   
   
Network Load Balancer (~100 ms) as ALB has a latency of ~400 ms   
   
## True or False? Network load balancer has one static IP per availability zone   
   
True.   
   
## What are the supported target groups for network load balancer?   
   
   
- EC2 instance   
- IP addresses   
- Application Load Balancer   
   
## What are the supported target groups for gateway load balancer?   
   
   
- EC2 instance   
- IP addresses (must be private IPs)   
   
## Name one use case for using application load balancer as a target group for network load balancer   
   
You might want to have a fixed IP address (NLB) and then forward HTTP traffic based on path, query, ... which is then done by ALB   
   
## What are some use cases for using Network Load Balancer?   
   
   
- TCP, UDP traffic   
- Extreme performance   
   
## True or False? Network load balancers operate in layer 4   
   
True. They forward TCP, UDP traffic.   
   
## True or False? It's possible to enable sticky session for network load balancer so the same client is always redirected to the same instance   
   
False. This is only supported in Classic Load Balancer and Application Load Balancer.   
   
## Explain Cross Zone Load Balancing   
   
With cross zone load balancing, traffic distributed evenly across all (registered) instances in all the availability zones.   
   
## True or False? For network load balancer, cross zone load balancing is always on and can't be disabled   
   
False. It's disabled by default   
   
## True or False? In regards to cross zone load balancing, AWS charges you for inter AZ data in network load balancer but no in application load balancer   
   
False. It charges for inter AZ data in network load balancer, but not in application load balancer   
   
## True or False? Both ALB and NLB support multiple listeners with multiple SSL certificates   
   
True   
   
## Explain Deregistration Delay (or Connection Draining) in regards to ELB   
   
The period of time or process of "draining" instances from requests/traffic (basically let it complete all active connections but don't start new ones) so it can be de-registered eventually and ELB won't send requests/traffic to it anymore.   
   
#### NLB   
   
## At what network level/layer a Network Load Balancer operates?   
   
Layer 4   
   
#### ALB   
   
## True or False? With ALB (Application Load Balancer) it's possible to do routing based on query string and/or headers   
   
True.   
   
## True or False? For application load balancer, cross zone load balancing is always on and can't be disabled   
   
True   
   
### Auto Scaling Group   
   
## Explain Auto Scaling Group   
   
[Amazon Docs](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html): "An Auto Scaling group contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. An Auto Scaling group also enables you to use Amazon EC2 Auto Scaling features such as health check replacements and scaling policies"   
   
## You have two instance running as part of ASG. You change the desired capacity to 1. What will be the outcome of this change?   
   
One of the instances will be terminated.   
   
## How can you customize the trigger for the scaling in/out of an auto scaling group?   
   
One way is to use CloudWatch alarms where an alarm will monitor a metric and based on a certain value (or range) you can choose to scale-in or scale-out the ASG.   
   
## What are some metrics/rules used for auto scaling   
   
   
- Network In/Out   
- Number of requests on ELB per instance   
- Average CPU, RAM usage   
   
## What is dynamic Scaling policy in regards to Auto Scaling Groups?   
   
A policy in which scaling will occur automatically based on different metrics.   
   
There are 3 types:   
   
1. Target Tracking Scaling: scale when the baseline changes (e.g. CPU is over 60%)   
2. Step Scaling: more granular scaling where you can choose different actions for different metrics values (e.g. when CPU less than 20%, remove one instance. When CPU is over 40%, add 3 instances)   
3. Scheduled Actions: set in advance scaling for specific period of time (e.g. add instances on Monday between 10:00 am to 11:00 am)   
   
## What is a predictive scaling policy in regards to Auto Scaling Groups?   
   
Scale by analyzing historical load and schedule scaling based on forecast load.   
   
## Explain scaling cooldowns in regards to Auto Scaling Groups   
   
During a scaling cooldown, ASG will not terminate or launch additional instances. The cooldown happens after scaling activity and the reason for this behaviour is that some metrics have to be collected and stabilize before another scaling operating can take place.   
   
## Explain the default ASG termination policy   
   
1. It finds the AZ which the most number of EC2 instances   
2. If number of instances > 1, choose the one with oldest launch configuration, template and terminate it   
   
## True or False? by default, ASG tries to balance the number of instances across AZ   
   
True, this is why when it terminates instances, it chooses the AZ with the most instances.   
   
## Explain Lifecycle hooks in regards to Auto Scaling Groups   
   
Lifecycle hooks allows you perform extra steps before the instance goes in service (During pending state) or before it terminates (during terminating state).   
   
## If you use ASG and you would like to run extra steps before the instance goes in service, what will you use?   
   
Lifecycle hooks in pending state.   
   
## Describe one way to test ASG actually works   
   
In Linux instances, you can install the 'stress' package and run stress to load the system for certain period of time and see if ASG kicks in by adding additional capacity (= more instances).   
   
For example: `sudo stress --cpu 100 --timeout 20`   
   
### Security   
   
## What is the shared responsibility model? What AWS is responsible for and what the user is responsible for based on the shared responsibility model?   
   
The shared responsibility model defines what the customer is responsible for and what AWS is responsible for.   
   
More on the shared responsibility model [here](https://aws.amazon.com/compliance/shared-responsibility-model)   
   
## True or False? Based on the shared responsibility model, Amazon is responsible for physical CPUs and security groups on instances   
   
False. It is responsible for Hardware in its sites but not for security groups which created and managed by the users.   
   
## Explain "Shared Controls" in regards to the shared responsibility model   
   
AWS definition: "apply to both the infrastructure layer and customer layers, but in completely separate contexts or perspectives. In a shared control, AWS provides the requirements for the infrastructure and the customer must provide their own control implementation within their use of AWS services"   
   
Learn more about it [here](https://aws.amazon.com/compliance/shared-responsibility-model)   
   
## What is the AWS compliance program?   
   
## How to secure instances in AWS?   
   
   
- Instance IAM roles should have minimal permissions needed. You don't want an instance-level incident to become an account-level incident   
- Use "AWS System Manager Session Manager" for SSH   
- Using latest OS images with your instances   
   
## What is AWS Artifact?   
   
AWS definition: "AWS Artifact is your go-to, central resource for compliance-related information that matters to you. It provides on-demand access to AWS’ security and compliance reports and select online agreements."   
   
Read more about it [here](https://aws.amazon.com/artifact)   
   
## What is AWS Inspector?   
   
AWS definition: "Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS. Amazon Inspector automatically assesses applications for exposure, vulnerabilities, and deviations from best practices.""   
   
Learn more [here](https://aws.amazon.com/inspector)   
   
## What is AWS Guarduty?   
   
AWS definition: "Amazon GuardDuty is a threat detection service that continuously monitors for malicious activity and unauthorized behavior to protect your Amazon Web Services accounts, workloads, and data stored in Amazon S3" <br>   
Monitor VPC Flow lows, DNS logs, CloudTrail S3 events and CloudTrail Mgmt events.   
   
## What is AWS Shield?   
   
AWS definition: "AWS Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS."   
   
## What is AWS WAF? Give an example of how it can used and describe what resources or services you can use it with   
   
## What AWS VPN is used for?   
   
## What is the difference between Site-to-Site VPN and Client VPN?   
   
## What is AWS CloudHSM?   
   
Amazon definition: "AWS CloudHSM is a cloud-based hardware security module (HSM) that enables you to easily generate and use your own encryption keys on the AWS Cloud."   
   
Learn more [here](https://aws.amazon.com/cloudhsm)   
   
## True or False? AWS Inspector can perform both network and host assessments   
   
True   
   
## What is AWS Key Management Service (KMS)?   
   
AWS definition: "KMS makes it easy for you to create and manage cryptographic keys and control their use across a wide range of AWS services and in your applications."   
More on KMS [here](https://aws.amazon.com/kms)   
   
## What is AWS Acceptable Use Policy?   
   
It describes prohibited uses of the web services offered by AWS.   
More on AWS Acceptable Use Policy [here](https://aws.amazon.com/aup)   
   
## True or False? A user is not allowed to perform penetration testing on any of the AWS services   
   
False. On some services, like EC2, CloudFront and RDS, penetration testing is allowed.   
   
## True or False? DDoS attack is an example of allowed penetration testing activity   
   
False.   
   
## True or False? AWS Access Key is a type of MFA device used for AWS resources protection   
   
False. Security key is an example of an MFA device.   
   
## What is Amazon Cognito?   
   
Amazon definition: "Amazon Cognito handles user authentication and authorization for your web and mobile apps."   
   
Learn more [here](https://docs.aws.amazon.com/cognito/index.html)   
   
## What is AWS ACM?   
   
Amazon definition: "AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources."   
   
Learn more [here](https://aws.amazon.com/certificate-manager)   
   
### Databases   
   
#### RDS   
   
## What is AWS RDS?   
   
   
- Relational Database Service   
- Managed DB service (you can't ssh the machine)   
- Supports multiple DBs: MySQL, Oracle, Aurora (AWS Proprietary), ...   
   
## Why to use AWS RDS instead of launching an EC2 instance and install a database on it?   
   
AWS RDS is a managed service, that means it's automatically provisioned and patched for you.   
   
In addition, it provides you with continuous backup (and the ability to restore from any point of time), scaling capability (both horizontal and vertical), monitoring dashboard and read replicas.   
   
## What do you know about RDS backups?   
   
   
- Automated backups   
- Full daily backup (done during maintenance window)   
- Transactions logs backup every 5 minutes   
- Retention can be increased and by default it's 7 days   
   
## Explain AWS RDS Storage Auto Scaling   
   
   
- RDS storage can automatically be increased upon lack in storage   
- The user needs to set "Maximum Storage Threshold" to have some limit on storage scaling   
- Use cases: applications with unpredictable workloads   
- Supports multiple RDS database engines   
   
## Explain Amazon RDS Read Replicas   
   
[AWS Docs](https://aws.amazon.com/rds/features/read-replicas): "Amazon RDS Read Replicas provide enhanced performance and durability for RDS database (DB) instances. They make it easy to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads."   
   
In simpler words, it allows you to scale your reads.   
   
## True or False? RDS read replicas are supported within az, cross az and cross region   
   
True   
   
## True or False? RDS read replicas are asynchronous   
   
True. This is done so the reads are consistent.   
   
## True or False? Amazon RDS supports MongoDB   
   
False. RDS is relational database and MongoDB is a NoSQL db.   
   
## What are some use cases for using RDS read replicas?   
   
You have a main application which works against your database but you would like to add additional app, one used for logging, analytics, ... so you prefer it won't use the same database. In this case, you create a read replica instance and the second application works against that instance.   
   
## Explain RDS Multi Availability Zone   
   
   
- RDS multi AZ used mainly for disaster recovery purposes   
- There is an RDS master instance and in another AZ an RDS standby instance   
- The data is synced synchronously between them   
- The user, application is accessing one DNS name and where there is a failure with the master instance, the DNS name moves to the standby instance, so the failover done automatically   
   
## True or False? Moving AWS RDS from single AZ to multi AZ is an operation with downtime (meaning there is a need to stop the DB)   
   
False. It's a zero downtime operation = no need to stop the database.   
   
## How AWS RDS switches from single AZ to multi AZ?   
   
1. Snapshot is taken by RDS   
2. The snapshot is restored to another, standby, RDS instance   
3. Synchronization is enabled between the two instances   
   
## True or False? RDS encryption should be defined at launch time   
   
True   
   
## True or False? in regards to RDS, replicas can be encrypted even if the master isn't encrypted   
   
False   
   
## How to make RDS snapshots encrypted?   
   
   
- If RDS database is encrypted then, the snapshot itself is also encrypted   
- If RDS database isn't encrypted then, the snapshot itself isn't encrypted and then you can copy the un-encrypted snapshot to created an encrypted copy   
   
## How to encrypt an un-encrypted RDS instance?   
   
Create a copy of the un-encrypted instance -> copy the snapshot to create an encrypted copy -> restore the database from the encrypted snapshot -> migrate the application to work against the copied instance -> remove the original DB instance   
   
## How IAM authentication works with RDS?   
   
For example:   
   
1. EC2 instance uses IAM role to make an API call to get auth token   
2. The token, with SSL encryption, is used for accessing the RDS instance   
   
Note: The token has a lifetime of 15 minutes   
   
## True or False? In case of RDS (not Aurora), read replicas require you to change the SQL connection string   
   
True. Since read replicas add endpoints, each with its own DNS name, you need to modify your app to reference these new endpoints to balance the load read.   
   
#### Aurora   
   
## What do you know about Amazon Aurora?   
   
   
- A MySQL & Postgresql based relational database.   
- Proprietary technology from AWS   
- The default database proposed for the user when using RDS for creating a database.   
- Storage automatically grows in increments of 10 GiB   
- HA native - failover in instant   
- Has better performances over MySQL and Postgres   
- Supports 15 replicas (while MySQL supports 5)   
   
## True or False? Aurora stores 4 copies of your data across 2 availability zones   
   
False. It stores 6 copies across 3 availability zones   
   
## True or False? Aurora support self healing where corrupted data replaced by doing peer-to-peer replication   
   
True   
   
## True or False? Aurora storage is striped across 20 volumes   
   
False. 100 volumes.   
   
## True or False? It's possible to scale Aurora replicas   
   
True. If your read replica instances exhaust their CPU, you can scale by adding more instances   
   
## Explain Aurora Serverless. What use cases is it good for?   
   
   
- Aurora serverless is an automated database instantiation and it's auto scaled based on an actual usage   
- It's good mainly for infrequent or unpredictable workflows   
- You pay per second so it can eventually be more cost effective   
   
## What is the use case for Aurora multi-master?   
   
Aurora multi-master is perfect for a use case where you want to have instant failover for write node.   
   
#### DynamoDB   
   
## What is AWS DynamoDB?   
   
## Explain "Point-in-Time Recovery" feature in DynamoDB   
   
Amazon definition: "You can create on-demand backups of your Amazon DynamoDB tables, or you can enable continuous backups using point-in-time recovery. For more information about on-demand backups, see On-Demand Backup and Restore for DynamoDB."   
   
Learn more [here](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/PointInTimeRecovery.html)   
   
## Explain "Global Tables" in DynamoDB   
   
Amazon definition: "A global table is a collection of one or more replica tables, all owned by a single AWS account."   
   
Learn more [here](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/V2globaltables_HowItWorks.html)   
   
## What is DynamoDB Accelerator?   
   
Amazon definition: "Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to a 10x performance improvement – from milliseconds to microseconds..."   
   
Learn more [here](https://aws.amazon.com/dynamodb/dax)   
   
#### ElastiCache   
   
## What is AWS ElastiCache? In what use case should it be used?   
   
Amazon Elasticache is a fully managed Redis or Memcached in-memory data store.<br>   
It's great for read-intensive workloads where the common data/queries are cached and apps/users access the cache instead of the primary database.   
   
## Describe the workflow of an application using the cache in AWS   
   
1. The application performs a query against the DB. There is a check to see if the data is in the cache   
1. If it is, it's a "cache hit" and the data is retrieved from there   
1. If it's not in there, it's a "cache miss" and the data is pulled from the database   
1. The data is then also written to the cache (assuming it is often accessed) and next time the user queries for the same data, it might be retrieved from the cache (depends on how much time passed and whether this specific data was invalidated or not)   
   
## How can you make an application stateless using ElastiCache?   
   
Let's say you have multiple instances running the same application and every time you use the application, it creates a user session.<br>   
This user session can be stored in ElastiCache so even if the user contacts a different instance of the application, the application can retrieve the session from the ElsatiCache.   
   
## You need a highly available cache with backup and restore features. Which one would you use?   
   
ElastiCache Redis.   
   
## You need a cache with read replicas that can be scaled and one support multi AZ. Which one would you use?   
   
ElastiCache Redis.   
   
## You need a cache that supports sharding and built with multi-threaded architecture in mind. Which one would you use?   
   
ElastiCache Memcached   
   
## True or False? ElastiCache doesn't supports IAM authentication   
   
True.   
   
## What patterns are there for loading data into the cache?   
   
   
- Write Through: add or update data in the cache when the data is written to the DB   
- Lazy Loading: all the read data is cached   
- Session Store: store temporary session data in cache   
   
#### RedShift   
   
## What is AWS Redshift and how is it different than RDS?   
   
cloud data warehouse   
   
## What do you if you suspect AWS Redshift performs slowly?   
   
   
- You can confirm your suspicion by going to AWS Redshift console and see running queries graph. This should tell you if there are any long-running queries.   
- If confirmed, you can query for running queries and cancel the irrelevant queries   
- Check for connection leaks (query for running connections and include their IP)   
- Check for table locks and kill irrelevant locking sessions   
   
## What is Amazon DocumentDB?   
   
Amazon definition: "Amazon DocumentDB (with MongoDB compatibility) is a fast, scalable, highly available, and fully managed document database service that supports MongoDB workloads. As a document database, Amazon DocumentDB makes it easy to store, query, and index JSON data."   
   
Learn more [here](https://aws.amazon.com/documentdb)   
   
## What "AWS Database Migration Service" is used for?   
   
## What type of storage is used by Amazon RDS?   
   
EBS   
   
### Identify the Service   
   
## What would you use for automating code/software deployments?   
   
AWS CodeDeploy   
   
## You would like to invoke a function every time you enter a URL in the browser. Which service would you use for that?   
   
AWS Lambda   
   
## What would you use for easily creating similar AWS environments/resources for different customers?   
   
CloudFormation   
   
## Using which service, can you add user sign-up, sign-in and access control to mobile and web apps?   
   
Cognito   
   
## Which service would you use for building a website or web application?   
   
Lightsail   
   
## Which tool would you use for choosing between Reserved instances or On-Demand instances?   
   
Cost Explorer   
   
## What would you use to check how many unassociated Elastic IP address you have?   
   
Trusted Advisor   
   
## Which service allows you to transfer large amounts (Petabytes) of data in and out of the AWS cloud?   
   
AWS Snowball   
   
## Which service would you use if you need a data warehouse?   
   
AWS RedShift   
   
## Which service provides a virtual network dedicated to your AWS account?   
   
VPC   
   
## What you would use for having automated backups for an application that has MySQL database layer?   
   
Amazon Aurora   
   
## What would you use to migrate on-premise database to AWS?   
   
AWS Database Migration Service (DMS)   
   
## What would you use to check why certain EC2 instances were terminated?   
   
AWS CloudTrail   
   
## What would you use for SQL database?   
   
AWS RDS   
   
## What would you use for NoSQL database?   
   
AWS DynamoDB   
   
## What would you use for adding image and video analysis to your application?   
   
AWS Rekognition   
   
## Which service would you use for debugging and improving performances issues with your applications?   
   
AWS X-Ray   
   
## Which service is used for sending notifications?   
   
SNS   
   
## What would you use for running SQL queries interactively on S3?   
   
AWS Athena   
   
## What would you use for preparing and combining data for analytics or ML?   
   
AWS Glue   
   
## Which service would you use for monitoring malicious activity and unauthorized behavior in regards to AWS accounts and workloads?   
   
Amazon GuardDuty   
   
## Which service would you use for centrally manage billing, control access, compliance, and security across multiple AWS accounts?   
   
AWS Organizations   
   
## Which service would you use for web application protection?   
   
AWS WAF   
   
## You would like to monitor some of your resources in the different services. Which service would you use for that?   
   
CloudWatch   
   
## Which service would you use for performing security assessment?   
   
AWS Inspector   
   
## Which service would you use for creating DNS record?   
   
Route 53   
   
## What would you use if you need a fully managed document database?   
   
Amazon DocumentDB   
   
## Which service would you use to add access control (or sign-up, sign-in forms) to your web/mobile apps?   
   
AWS Cognito   
   
## Which service is often reffered to as "used for decoupling applications"?   
   
AWS SQS. Since it's a messaging queue so it allows applications to switch from synchronous communication to asynchronous one.   
   
## Which service would you use if you need messaging queue?   
   
Simple Queue Service (SQS)   
   
## Which service would you use if you need managed DDOS protection?   
   
AWS Shield   
   
## Which service would you use if you need store frequently used data for low latency access?   
   
ElastiCache   
   
## What would you use to transfer files over long distances between a client and an S3 bucket?   
   
Amazon S3 Transfer Acceleration   
   
## Which services are involved in getting a custom string (based on the input) when inserting a URL in the browser?   
   
Lambda - to define a function that gets an input and returns a certain string<br>   
API Gateway - to define the URL trigger (= when you insert the URL, the function is invoked).   
   
## Which service would you use for data or events streaming?   
   
Kinesis   
   
## Which (free) tool would you use to get information on cost savings?   
   
Trusted Advisor   
   
## You would like to have on-perm storage access to AWS storage. What would you use for that?   
   
Storage Gateway   
   
### DNS (Route 53)   
   
## What is Route 53?   
   
[AWS Route 53](https://aws.amazon.com/route53): "Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service..."   
   
Some of Route 53 features:   
   
   
- Register domains   
- DNS service - domain name translations   
- Health checks - verify your app is available   
- Not a feature but its SLA is 100% availability   
   
## What it means that "Route 53 is an Authoritative DNS"?   
   
The customer can update DNS records   
   
## What each Route 53 record contains?   
   
   
- Domain/subdomain name (e.g. blipblop.com)   
- Value (e.g. 201.7.202.2)   
- Record type (e.g. A, AAAA, MX)   
- TTL: amount of time the record is going to be cached   
- Routing Policy: how to respond to queries   
   
## What DNS record types does Route 53 supports?   
   
   
- A   
- AAAA   
- CNAME   
- NS   
- DS   
- CAA   
- SOA   
- MX   
- TXT   
- SPF   
- SRV   
- NAPTR   
- PTR   
   
## What are hosted zones?   
   
A container that includes records for defining how to route traffic from a domain and its subdomains   
   
## What types of hosted zones are there?   
   
   
- Public Hosted Zones - include records to specify how to route traffic on the internet   
- Private Hosted Zones - contain records that specify how you traffic within VPC(s)   
   
## What is the difference between CNAME record and an Alias record?   
   
CNAME is used for mapping one hostname to any other hostname while Alias is used to map an hostname to an AWS resource.   
   
In addition, Alias work for both root domain (somedomain.com) and non-root domain, while CNAME works only with non-root domain (foo.somedomain.com)   
   
## True or False? Alias record can be set up for an EC2 DNS name   
   
False   
   
## True or False? Alias record can be set up for an VPC interface endpoint   
   
True   
   
## True or False? Alias record is only of type A or AAAA   
   
True   
   
## What is a routing policy in regards to AWS Route 53?   
   
A routing policy routing defines how Route 53 responds to DNS queries.   
   
## What Route 53 routing policies are there?   
   
   
- Simple   
- Geolocation   
- Failover   
- Latency based   
- Geoproximity   
- Multi-Value Answer   
- Weighted   
   
## Suppose you need to route % of your traffic to a certain instance and the rest of the traffic, to another instance. Which routing policy would you choose?   
   
Weighted routing policy.   
   
## Suppose you need to route traffic to a single source with Route 53, without any other requirements, which routing policy would you choose?   
   
The `simple` routing policy   
   
## Explain the geolocation routing policy   
   
   
- Routing based on user location   
- Location can be specified by continent, country or US state   
- It's recommended to have a default record in case there is no match on location   
   
## What are some use cases for using geolocation routing policy?   
   
   
- Restrict content distribution   
- App localization   
- Load balancing   
   
## Explain the geoproximity routing policy   
   
   
- Route based on the geographic location of resources   
- Shifting routing is done based on the `bias` value   
- Resources can be of AWS and non-AWS type   
  - For non-AWS you have to specify latitude and longitude in addition to AWS region as done in AWS-based resources   
- To use it, you have to use Route 53 traffic flow   
   
## What are some use cases for <code>weighted</code> routing policy?   
   
   
- Load balancing between regions   
- Testing new applications versions   
   
## True or False? Route 53 <code>simple</code> routing policy supports both single and multiple values   
   
True.   
   
If multiple values are returned from Route 53 then, the client chooses a single value to use.   
   
## True or False? In <code>weighted</code> routing DNS records must have the same name but not the same type   
   
False. They must have the same name AND type.   
   
## You would like to use a routing policy that will take latency into account and will route to the resource with the lowest latency. Which routing policy would you use?   
   
Latency-based routing policy.   
   
## What happens when you set all records to weight 0 when using <code>Weighted</code> routing policy?   
   
All records are used equally.   
   
## What Route 53 health checks are used for?   
   
Automated DNS failover based on monitoring:   
   
   
- Another health check   
- endpoint (app, AWS resource, server)   
- CloudWatch alarms   
   
## You would like to use a routing policy based on the resource location and be able to shift more traffic to some resources. Which one would you use?   
   
Geoproximity routing policy   
   
## Explain Route 53 Traffic Flow feature   
   
It's a visual editor for managing complex routing decision trees. It allows you to simplify the process of managing records.   
   
Configuration can be saved (as Traffic Flow Policy) and applied to different domains/hosted zones. In addition, it supports versioning   
   
## What are calculated health checks?   
   
When you combine the results of multiple health checks into a single health check.   
   
## What is one possible use case for using calculated health checks?   
   
Performing maintenance for a website without causing all the health checks to fail.   
   
## You would like to use a routing policy based on the user location. Which one would you use?   
   
Geolocation routing policy. It's based on user location.   
   
Don't confuse it with latency-based routing policy. While shorter distance may result in lower latency, this is not the requirement in the question.   
   
## True or False? Route 53 Multi Value is a substitute for those who want cheaper solution than ELB   
   
False. Route 53 Multi Value is not a substitute for ELB. It's focused on client-side load balancing as opposed to ELB.   
   
## True or False? Domain registrar and DNS service is inherently the same thing   
   
False. DNS service can be Route 53 (where you manage DNS records) while the domain itself can be purchased from other sources that aren't Amazon related (e.g. GoDadday).   
   
### SQS   
   
## What is Simple Queue Service (SQS)?   
   
AWS definition: "Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications".   
   
Learn more about it [here](https://aws.amazon.com/sqs)   
   
## Explain "producer" and "consumer" in regards to messaging queue   
   
Producer is the application or in general, the source that sends messages to the queue.   
   
Consumer is the process or application that pulls the messages from the queue.   
   
## What "default retention of messages" means?   
   
It refers to a retention period in which a message has to consumed/processed and deleted from the queue.   
   
As of today, the retention of a message is 4 days by default and the maximum allows is 14 days.   
   
## What's the limitation on message size in SQS?   
   
   
- 128KB   
- 128MB   
- 256KB   
- 256MB   
   
256KB   
   
## True or False? It's possible to have duplicated messages in the queue   
   
True. It's referred to as "at least once delivery".   
   
## True or False? "Consumers" can be only EC2 instances   
   
False. They can be Lambda functions and even on-premise instances   
   
## True or False? Processes/Applications use from the SDK the SendMessage API in order to send messages to the queue   
   
True.   
   
## What it means "best effort ordering" in regards to SQS?   
   
It means messages in the queue can be out of order.   
   
## What is "Delay Queue" in regards to SQS?   
   
It's the time in seconds to delay the delivery of new messages (when they reached the queue already).   
   
The limit as of today is 15 minutes.   
   
## What is "Visibility Timeout?"   
   
The time in seconds for a message to not be visible for consumers.   
   
The limit as of today is 12 hours   
   
## Give an example of architecture or workflow that involves SQS and EC2 & S3   
   
A website that allows users to upload videos and adds subtitles to them:   
   
1. First the user uploads the video through the web interface which uploads it to an S3 bucket   
2. SQS gets notified with a message on the video location   
3. EC2 instance (or Lambda function) starts to work on adding the subtitles   
4. The video with the subtitles is uploaded to an S3 buckets   
5. SQS gets notified of the result and specifically the video location   
   
## What's MessageGroupID?   
   
### SNS   
   
## What is Simply Notification Service?   
   
AWS definition: "a highly available, durable, secure, fully managed pub/sub messaging service that enables you to decouple microservices, distributed systems, and serverless applications."   
   
Read more about it [here](https://aws.amazon.com/sns)   
   
## Explain the following in regards to SNS:   
   
   
- Topics   
- Subscribers   
- Publishers   
   
* Topics - used for grouping multiple endpoints   
* Subscribers - the endpoints where topics send messages to   
* Publishers - the provider of the message (event, person, ...)   
   
## How SNS is different from SQS?   
   
SNS, as opposed to SQS, works in a publisher/subscriber model. Where's SQS works in Producer/Consumer model.   
   
SQS delivers the message to one consumer where's SNS will send a message to multiple subscribers.   
   
## What's a Fan-Out pattern?   
   
A messaging pattern where a single message is send to multiple destinations (often simultaneously). So one-to-many broadcast message.   
   
### Monitoring and Logging   
   
## What is AWS CloudWatch?   
   
AWS definition: "Amazon CloudWatch is a monitoring and observability service..."   
   
More on CloudWatch [here](https://aws.amazon.com/cloudwatch)   
   
## What is AWS CloudTrail?   
   
AWS definition: "AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account."   
   
Read more on CloudTrail [here](https://aws.amazon.com/cloudtrail)   
   
### Billing and Support   
   
## What are Service Control Policies and to what service they belong?   
   
AWS organizations service and the definition by Amazon: "SCPs offer central control over the maximum available permissions for all accounts in your organization, allowing you to ensure your accounts stay within your organization’s access control guidelines."   
   
Learn more [here](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scp.html)   
   
## Explain AWS pricing model   
   
It mainly works on "pay-as-you-go" meaning you pay only for what are using and when you are using it.   
In s3 you pay for 1. How much data you are storing 2. Making requests (PUT, POST, ...)   
In EC2 it's based on the purchasing option (on-demand, spot, ...), instance type, AMI type and the region used.   
   
More on AWS pricing model [here](https://aws.amazon.com/pricing)   
   
## How do you estimate AWS costs?   
   
   
- TCO calculator   
- AWS simple calculator   
- Cost Explorer   
- AWS Budgets   
- Cost Allocation Tags   
   
## What basic support in AWS includes?   
   
   
- 24x7 customer service   
- Trusted Advisor   
- AWS personal Health Dashoard   
   
## How are EC2 instances billed?   
   
## What AWS Pricing Calculator is used for?   
   
## What is Amazon Connect?   
   
Amazon definition: "Amazon Connect is an easy to use omnichannel cloud contact center that helps companies provide superior customer service at a lower cost."   
   
Learn more [here](https://aws.amazon.com/connect)   
   
## What are "APN Consulting Partners"?   
   
Amazon definition: "APN Consulting Partners are professional services firms that help customers of all types and sizes design, architect, build, migrate, and manage their workloads and applications on AWS, accelerating their journey to the cloud."   
   
Learn more [here](https://aws.amazon.com/partners/consulting)   
   
## Which of the following are AWS accounts types (and are sorted by order)?   
   
   
- Basic, Developer, Business, Enterprise   
- Newbie, Intermediate, Pro, Enterprise   
- Developer, Basic, Business, Enterprise   
- Beginner, Pro, Intermediate Enterprise   
   
   
- Basic, Developer, Business, Enterprise   
   
## True or False? Region is a factor when it comes to EC2 costs/pricing   
   
True. You pay differently based on the chosen region.   
   
## What is "AWS Infrastructure Event Management"?   
   
AWS Definition: "AWS Infrastructure Event Management is a structured program available to Enterprise Support customers (and Business Support customers for an additional fee) that helps you plan for large-scale events such as product or application launches, infrastructure migrations, and marketing events."   
   
#### AWS Organizations   
   
## What is "AWS Organizations"?   
   
AWS definition: "AWS Organizations helps you centrally govern your environment as you grow and scale your workloads on AWS."   
   
Read more on Organizations [here](https://aws.amazon.com/organizations)   
   
## What's an OU in regards to AWS Organizations?'   
   
OU (Organizational Units) is a way to group multiple accounts together so you can treat them as a single unit.   
   
By default there is the "Root" OU created in AWS Organizations.   
   
Most of the time OUs are based on functions or common set of controls.   
   
### Automation   
   
## What is AWS CodeDeploy?   
   
Amazon definition: "AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers."   
   
Learn more [here](https://aws.amazon.com/codedeploy)   
   
## Explain what is CloudFormation   
   
AWS definition: "AWS CloudFormation is a service that helps you model and set up your Amazon Web Services resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of provisioning and configuring those resources for you."   
   
## What is AWS CDK?   
   
AWS definition: "The AWS Cloud Development Kit (AWS CDK) is an open-source software development framework to define cloud infrastructure as code and provision it through AWS CloudFormation. CDK gives the flexibility to use popular programming languages like TypeScript, JavaScript, Python, Java, C# and Go (in Developer Preview) to define your infrastructure, and AWS CDK provides a set of libraries for AWS services that abstract away the need to write raw CloudFormation templates.   
   
Learn more [here](https://aws.amazon.com/cdk)   
   
### Misc   
   
## Which AWS service you have experience with that you think is not very common?   
   
## What is AWS CloudSearch?   
   
## What is AWS Lightsail?   
   
AWS definition: "Lightsail is an easy-to-use cloud platform that offers you everything needed to build an application or website, plus a cost-effective, monthly plan."   
   
## What is AWS Rekognition?   
   
AWS definition: "Amazon Rekognition makes it easy to add image and video analysis to your applications using proven, highly scalable, deep learning technology that requires no machine learning expertise to use."   
   
Learn more [here](https://aws.amazon.com/rekognition)   
   
## What AWS Resource Groups used for?   
   
Amazon definition: "You can use resource groups to organize your AWS resources. Resource groups make it easier to manage and automate tasks on large numbers of resources at one time. "   
   
Learn more [here](https://docs.aws.amazon.com/ARG/latest/userguide/welcome.html)   
   
## What is AWS Global Accelerator?   
   
Amazon definition: "AWS Global Accelerator is a service that improves the availability and performance of your applications with local or global users..."   
   
Learn more [here](https://aws.amazon.com/global-accelerator)   
   
## What is AWS Config?   
   
Amazon definition: "AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources."   
   
Learn more [here](https://aws.amazon.com/config)   
   
## What is AWS X-Ray?   
   
AWS definition: "AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture."   
Learn more [here](https://aws.amazon.com/xray)   
   
## What is AWS OpsWorks?   
   
Amazon definition: "AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet."   
   
Learn more about it [here](https://aws.amazon.com/opsworks)   
   
## What is AWS Snowmobile?   
   
"AWS Snowmobile is an Exabyte-scale data transfer service used to move extremely large amounts of data to AWS."   
   
Learn more [here](https://aws.amazon.com/snowmobile)   
   
## What is AWS Athena?   
   
"Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL."   
   
Learn more about AWS Athena [here](https://aws.amazon.com/athena)   
   
## What is Amazon Cloud Directory?   
   
Amazon definition: "Amazon Cloud Directory is a highly available multi-tenant directory-based store in AWS. These directories scale automatically to hundreds of millions of objects as needed for applications."   
   
Learn more [here](https://docs.aws.amazon.com/clouddirectory/latest/developerguide/what_is_cloud_directory.html)   
   
## What is AWS Elastic Beanstalk?   
   
AWS definition: "AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services...You can simply upload your code and Elastic Beanstalk automatically handles the deployment"   
   
Learn more about it [here](https://aws.amazon.com/elasticbeanstalk)   
   
## What is AWS SWF?   
   
Amazon definition: "Amazon SWF helps developers build, run, and scale background jobs that have parallel or sequential steps. You can think of Amazon SWF as a fully-managed state tracker and task coordinator in the Cloud."   
   
Learn more on Amazon Simple Workflow Service [here](https://aws.amazon.com/swf)   
   
## What is AWS EMR?   
   
AWS definition: "big data platform for processing vast amounts of data using open source tools such as Apache Spark, Apache Hive, Apache HBase, Apache Flink, Apache Hudi, and Presto."   
   
Learn more [here](https://aws.amazon.com/emr)   
   
## What is AWS Quick Starts?   
   
AWS definition: "Quick Starts are built by AWS solutions architects and partners to help you deploy popular technologies on AWS, based on AWS best practices for security and high availability."   
   
Read more [here](https://aws.amazon.com/quickstart)   
   
## What is the Trusted Advisor?   
   
Amazon definition: "AWS Trusted Advisor provides recommendations that help you follow AWS best practices. Trusted Advisor evaluates your account by using checks. These checks identify ways to optimize your AWS infrastructure, improve security and performance, reduce costs, and monitor service quotas."   
   
Learn more [here](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/)   
   
## What is AWS Service Catalog?   
   
Amazon definition: "AWS Service Catalog allows organizations to create and manage catalogs of IT services that are approved for use on AWS."   
   
Learn more [here](https://aws.amazon.com/servicecatalog)   
   
## What is AWS CAF?   
   
Amazon definition: "AWS Professional Services created the AWS Cloud Adoption Framework (AWS CAF) to help organizations design and travel an accelerated path to successful cloud adoption. "   
   
Learn more [here](https://aws.amazon.com/professional-services/CAF)   
   
## What is AWS Cloud9?   
   
AWS: "AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser"   
   
## What is AWS CloudShell?   
   
AWS: "AWS CloudShell is a browser-based shell that makes it easy to securely manage, explore, and interact with your AWS resources."   
   
## What is AWS Application Discovery Service?   
   
Amazon definition: "AWS Application Discovery Service helps enterprise customers plan migration projects by gathering information about their on-premises data centers."   
   
Learn more [here](https://aws.amazon.com/application-discovery)   
   
## What is the AWS well-architected framework and what pillars it's based on?   
   
AWS definition: "The Well-Architected Framework has been developed to help cloud architects build secure, high-performing, resilient, and efficient infrastructure for their applications. Based on five pillars — operational excellence, security, reliability, performance efficiency, and cost optimization"   
   
Learn more [here](https://aws.amazon.com/architecture/well-architected)   
   
## What AWS services are serverless (or have the option to be serverless)?   
   
AWS Lambda   
AWS Athena   
   
### High Availability   
   
## What high availability means from AWS perspective?   
   
   
- Application/Service is running in at least 2 availability zones   
- Application/Service should survive (= operate as usual) a data center disaster   
   
### Production Operations and Migrations   
   
## Describe in high-level how to upgrade a system on AWS with (near) zero downtime   
   
One way is through launching a new instance. In more detail:   
   
1. Launch a new instance   
2. Install all the updates and applications   
3. Test the instance   
4. If all tests passed successfully, you can start using the new instance and perform the switch with the old one, in one of various ways:   
5. Go to route53 and update the record with the IP of the new instance   
6. If you are using an Elastic IP then move it to the new instance   
   ...   
   
## You try to use an detached EBS volume from us-east-1b in us-east-1a, but it fails. What might be the reason?   
   
EBS volumes are locked to a specific availability zone. To use them in another availability zone, you need to take a snapshot and restore it in the destination availability zone.   
   
## When you launch EC2 instances, it takes them time to boot due to commands you run with user data. How to improve instances boot time?   
   
Consider creating customized AMI with the commands from user data already executed there. This will allow you launch instance instantly.   
   
## You try to mount EFS on your EC2 instance and it doesn't work (hangs...) What might be a possible reason?   
   
Security group isn't attached to your EFS or it lacks a rule to allow NFS traffic.   
   
## How to migrate an EBS volume across availability zones?   
   
1. Pause the application   
2. Take a snapshot of the EBS volume   
3. Restore the snapshot in another availability zone   
   
## How to encrypt an unencrypted EBS volume attached to an EC2 instance?   
   
1. Create EBS snapshot of the volume   
2. Copy the snapshot and mark the "Encrypt" option   
3. Create a new EBS volume out of the encrypted snapshot   
   
## You've created a network load balancer but it doesn't work (you can't reach your app on your EC2 instance). What might be a possible reason?   
   
Missing security group or misconfigured one.   
For example, if you go to your instances in the AWS console you might see that the instances under your NLB are in "unhealthy status" and if you didn't create a dedicated security group for your NLB, that means that the security group used is the one attached to the EC2 instances.   
   
Go to the security group of your instance(s) and enable the traffic that NLB should forward (e.g. TCP on port 80).   
   
### Scenarios   
   
## You have a load balancer running and behind it 5 web servers. Users complain that every time they move to a new page, they have to authenticate, instead of doing it once. How can you solve it?   
   
Enable sticky sessions. This way, the user keep working against the same instance, instead of being redirected to a different instance every request.   
   
## You have a load balancer running and behind it 5 web servers. Users complain that some times when they try to use the application it doesn't works. You've found out that sometimes some of the instances crash. How would you deal with it?   
   
One possible way is to use health checks with the load balancer to ensure the instances are ready to be used before forwarding traffic to them.   
   
## You run your application on 5 EC2 instances on one AZ and on 10 EC2 instances in another AZ. You distribute traffic between all of them using a network load balancer, but it seems that instances in one AZ have higher CPU rates than the instances in the other AZ. What might be the issue and how to solve it?   
   
It's possible that traffic is distributed evenly between the AZs but that doesn't mean it's distributed equally across all instances evenly.   
   
To distribute it evenly between all the instances, you have to enable cross-zone load balancing.   
   
## You are running an ALB that routes traffic using two hostnames: a.b.com and d.e.com. Is it possible to configure HTTPS for both of the hostnames?   
   
Yes, using SNI (Server Name Indication) each application can has its own SSL certificate (This is supported from 2017).   
   
## You have set up read replicas to scale reads but users complain that when they update posts in forums, the posts are not being updated. What may cause this issue?   
   
Read Replicas use asynchronous replication so it's possible users access a read replica instance that wasn't synced yet.   
   
## You need a persistent shared storage between your containers that some are running in Fargate and some in ECS. What would you use?   
   
EFS. It allows us to have persistent multi-AZ shared storage for containers.   
   
## You would like to run an AWS Fargate task every time a file is uploaded to a certain S3 bucket. How would you achieve that?   
   
Use Amazon EventBridge so every time a file is uploaded to an S3 bucket (event) it will run an ECS task.   
   
Such task should have an ECS Task Role so it can get the object from the S3 bucket (and possibly other permissions if it needs to update the DB for example).   
   
## Your hosts scale down and then back up quite often. What's your take on that?   
   
Often circular scaling (scale down, up and vice versa) is not a sign that the threshold set for scaling down and up are met quite often. In most cases that's a sign for you to adjust the threshold so scaling down doesn't happen as often.   
   
### Architecture Design   
   
## You've been asked to design an architecture for high performance and low-latency application (millions of requests per second). Which load balancer would you use?   
   
Network Load Balancer   
   
## What should you use for scaling reads?   
   
You can use an ElastiCache cluster or RDS Read Replicas.   
   
## You have two applications who communicate synchronously. It worked fine until there suddenly a spike of traffic. What change you might apply in this case?   
   
More details are missing to determine for sure but it might be better to decouple the applications by introducing one of the following:   
   
   
- Queue model with SQS   
- Publisher/Subscriber model with SNS   
   
### Misc   
   
## What's an ARN?   
   
ARN (Amazon Resources Names) used for uniquely identifying different AWS resources.   
It is used when you would like to identify resource uniqely across all AWS infra.