---
created: 1655707734273
desc: ''
id: 8io7ikmud38hlpv4vqm3f7r
title: AWS Fargate
updated: 1656161094367
---
   
AWS Fargate is a service that provisions serverless compute resources to run AWS ECS and EKS containers. AWS states that Fargate allows you to focus on building your applications when you let Fargate provision and manage the infrastructure required. Think of it as containers on-demand with no underlying manually created infrastructure that are quick to launch and scale, where you manage everything at the container level.   
   
You specify the resources your application needs to run and Fargate handles the provisioning of compute resources in an isolated and secure instance.   
   
Fargate determines the correct amount of compute resources required, which means you don’t need to worry about selecting instance types or having to scale the cluster capacity.   
   
With Fargate you only pay for the resources required to run your containers as they are consumed which means you eliminate over provisioning and paying for servers you don’t need.   
   
Fargate tasks (pods) run in their own kernels providing a secure and isolated compute environment, which provides an isolated workload and improved security as a consequence.   
   
Via - [What is AWS Fargate?](https://www.hava.io/blog/what-is-aws-fargate)   
   
## [AWS ECS](../devlog/AWS%20ECS.md) with [AWS fargate](../devlog/AWS%20Fargate.md)   
   
What if you want to delegate the management of infrastructure(virtual machines etc) also to AWS?   
   
Container lifecycle is being managed by AWS ECS but hosting can also be managed by AWS - for which you can use [AWS Fargate](../devlog/AWS%20Fargate.md).   
   
It is essentially an alternative to [aws.EC2](../devlog/aws.EC2.md) instances. Instead of creating EC2 instances and connecting the two with ECS cluster, you can create Fargate instance and connect that to the ECS cluster.   
   
It is a serverless way to launch containers. You take a container that you want to deploy on AWS and manage by ECS. You hand over the container to Fargate, you don't need to launch/provision any virtual machines/servers on your AWS account.   
   
Fargate will take your container and analyze it to check how much resources your container needs to run and it'll provision a server/resources for that specific container and deploy it and run it.   
   
It is on-demand, you don't need to provision or manage servers; you only have the infrastructure resources needed to run your containers. You only pay for the resources your containers are consuming. It scales very easily as it doesn't have fixed resources cap defined beforehand.   
   
However, if you need access to the underlying infrastructure for whatever reasons, EC2 offers more flexibility in that domain.   
   
Since you're using ECS for managing your containers and Fargate for managing your infrastructure needed for those containers, you can integrate your setup with other AWS services like [aws.CloudWatch](../devlog/aws.CloudWatch.md) for monitoring, [aws.IAM](../devlog/aws.IAM.md) for Users and Permissions, [AWS ELB](../devlog/AWS%20ELB.md) for [load balancer](/not_created.md), [aws.VPC](../devlog/aws.VPC.md) for networking etc.   
   
You can use Fargate Spot, a new capability that can run interruption-tolerant ECS Tasks at up to a 70% discount off the Fargate price.   
   
**Cons:**   
   
ECS + Fargate supports only one networking mode – _awsvpc_ – which limits your control over the networking layer (and you might need that in some scenarios).   
   
**Cost:** You’re charged based on the CPU and memory you select. The amount of CPU cores and GB determines the cost of running your cluster.   
   
See: [aws.EKS](../devlog/aws.EKS.md)