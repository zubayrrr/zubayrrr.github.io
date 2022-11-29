---
created: 1661426659846
desc: ''
id: ojhef2cmz0yh0p1akrr98sy
title: Create EKS cluster with eksctl
updated: 1661426659845
---
   
Topics::  [kubernetes](../devlog/kubernetes.md)   
   
---   
We’ve seen how to [aws.eks.Create EKS cluster with AWS Management Console](../devlog/aws.eks.Create%20EKS%20cluster%20with%20AWS%20Management%20Console.md) and [aws.eks.Create EKS Cluster with Fargate](../devlog/aws.eks.Create%20EKS%20Cluster%20with%20Fargate.md)   
   
Manually creating EKS cluster has disadvantages like not being able to replicate the whole thing.   
   
We can also achieve it using [aws.cli](../devlog/aws.cli.md).   
   
But let see how we can accomplish the same with `eksctl`.   
   
`eksctl` is a command line tool for working with EKS clusters that automates many individual tasks. Using this tool we can avoid having to create the different Roles, VPC etc.   
   
We simply execute a single command and all the necessary components get created and configured in the background. With the cli options we can customize the cluster for things like region, K8s version, EC2 instance types, Node Group or Fargate for Worker Nodes etc.   
   
## Configure `eksctl`   
   
Install `eksctl` from [eksctl.io](https://eksctl.io/introduction/#installation).   
   
Connect `eksctl` with the AWS account with credentials.   
   
It uses the same credentials that you configured for [aws.cli](../devlog/aws.cli.md). Checking for existing credentials `aws configure list` or `aws configure` to start configuring.   
   
## Create cluster   
   
`eksctl create cluster` takes default parameters and creates a cluster.   
   
**Create cluster with custom parameters**   
   
```bash
eksctl create cluster \
--name demo-cluster \
--version 1.17 \
--region eu-west-3
--nodegroup-name demo-nodes \
--node-type t2.micro \
--nodes 2 \
--nodes-min 2 \ # for autoscaler
--nodes-max 3 \
# there are other options like pub-key for Worker Nodes
```
   
   
Instead of using cli options you can also create a config file in [languages.YAML](../devlog/languages.YAML.md) and use it just like you’d use with `kubectl`.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662709222/wiki/s63fpwlhia2vqvmsmjp5.png)   
   
For other options check the [documentation](eksctl.io).   
   
Once executed, the command may take more than a few minutes to get fully initialized.   
   
You can use `eksctl` for also managing the cluster not just for creating it.   
   
## Review created cluster   
   
After the command is fully executed, it’ll save a new kubeconfig to `~/.kube/config`.   
   
To check what was created under the hood, from management console check:   
   
   
- IAM Roles - you’ll find 2 new roles.   
	- Node Group Role.   
	- Cluster Service Role with a managed and 2 inline policies.   
- VPC - a new VPC, public and private subnet pairs in 3 AZs will be created.   
- EC2 instances - new instances will be created as defined, check the “Workloads” tab to find what processes are running on those Worker Nodes.