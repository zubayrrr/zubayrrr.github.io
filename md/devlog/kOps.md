---
created: 1656161298524
desc: ''
id: fhi59s6yqplah2w1hfx9i5x
title: kOps
updated: 1656161663709
---
   
Kops is short for [Kubernetes](../devlog/kubernetes.md) Operations (also spelled kops or kOps), a set of tools AWS offers for installing, operating, and deleting Kubernetes clusters.   
   
You can also use it to roll out an upgrade of an older version of Kubernetes to a new one and manage cluster add-ons. After creating a cluster, you can use the usual kubectl CLI to manage resources.   
   
To quote the documentation:   
   
> kops will not only help you create, destroy, upgrade and maintain production-grade, highly available, Kubernetes cluster, but it will also provision the necessary cloud infrastructure.   
   
Key features of Kops:   
   
   
- Kops simplifies Kubernetes cluster setup and management, especially in comparison to the amount of effort needed to manually set up master and worker nodes.   
- It automates the provisioning of Highly Available Kubernetes clusters.   
- The tool manages Route53, AutoScaling Groups, ELBs for many different tasks from master and node bootstrapping to the API server and rolling updates to your cluster.   
- It’s multi-architecture ready and supports ARM64.   
- It supports multiple cloud platforms, which makes it a better choice if you’re afraid of getting locked into a specific Kubernetes offering.   
- It’s an open-source tool, so you can use it for free. However, you still need to pay for and maintain the underlying infrastructure created by Kops to manage your cluster.   
   
Via - [AWS EKS vs. ECS vs. Fargate vs. Kops: Where to Manage Your Kubernetes in 2022? - CAST AI – Kubernetes Automation Platform](https://cast.ai/blog/aws-eks-vs-ecs-vs-fargate-where-to-manage-your-kubernetes/)   
   
Kops does the job much faster. It’s a CLI tool you need to install on your local machine together with kubectl. To get a cluster running, use the Kops create cluster command. The great thing about Kops is that it manages most of the AWS resources you need for your Kubernetes cluster.   
   
Contrary to EKS, Kops creates master nodes as EC2 instances – you can always access them directly to make modifications around the networking layer, size, etc. You can monitor these nodes directly too.   
   
Kops lets you create a cluster really fast, but managing it is more complicated. There’s much groundwork to cover for upgrading and replacing master nodes for new Kubernetes versions. Creating a new cluster in a new VPC with Kops might be easier than that.   
When it comes to maintenance tasks like adding, replacing, and upgrading worker nodes, Kops performs quite similarly to [aws.EKS](../devlog/aws.EKS.md). AutoScaling Groups come in handy here.