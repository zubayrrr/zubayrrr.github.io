---
created: 1656159335261
desc: ''
id: 3ozxwzvy9lv8t60yjvx45e9
title: VPC
updated: 1662891860576
---
   
Amazon VPC lets users provision a logically isolated section of the AWS Cloud where users can launch AWS resources in a virtual network that they define within a region.   
   
[aws.S3](../devlog/aws.S3.md) is an example of service that sits **outside** of a VPC.   
   
Within a region there are **availability zones**, you can use those availability zone by creating subnets and assigning subnets to those availability zones. A subnet is always assigned to one availability zone. It cannot span over multiple AZs. You can multiple subnets within same AZs.   
   
We can deploy resources such as [aws.EC2](../devlog/aws.EC2.md) in a subnet. There is such a thing called **VPC Router**. We can interact with it by configuring **route tables**. The VPC Router takes care of routing within the VPC and outside of VPC.   
   
To be able to access the internet, you also need an **Internet Gateway**. It is attached to your VPC. You only get one per VPC. It is used to send data out to the internet and in from the internet.   
   
We configure the route table with the Internet Gateway ID that tells it to send all the traffic that doesn't fit for one the networks in the route table to the internet gateway.   
   
You’ve a default VPC that AWS automatically creates for you in every region.   
   
You can create multiple VPCs within a region(5 by default, soft limit).   
   
Each VPC has a [CIDR](../devlog/cidr.md) block, overall block of address from which you then create the addresses you assign to the subnets.