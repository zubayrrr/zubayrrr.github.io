---
created: 1655885960862
desc: ''
id: ervusa6qabwyx7sbb1a4vcg
title: EKS
updated: 1662727398480
---
   
Elastic [Kubernetes](../devlog/kubernetes.md) Service   
   
It is an alternative to [AWS ECS](../devlog/AWS%20ECS.md).   
   
EKS is a service that provides and manages a [Kubernetes](../devlog/kubernetes.md) control plane on its own. You have no access to the master nodes on EKS since they’re under a special AWS account.   
   
To run a Kubernetes workload, EKS establishes the control plane and Kubernetes API in your managed AWS infrastructure and you’re good to go.   
   
At this point, you can deploy workloads using native K8s tools like kubectl, Kubernetes Dashboard, Helm, and Terraform.   
   
   
- You **don’t have to install, operate, and maintain** your Kubernetes control plane.   
- EKS allows you to **easily run tooling and plugins** developed by the Kubernetes open-source community.   
- EKS **automates load distribution and parallel processing** better than any DevOps engineer could.   
- Your Kubernetes assets integrate seamlessly with AWS services if you use EKS.   
- EKS uses VPC networking.   
- Any application running on EKS is compatible with one running in your existing Kubernetes environment. You can migrate to EKS without applying any changes to the code.   
- Supports **EC2 spot instances** using managed node groups that follow spot best practices and allow some pretty great cost savings.   
   
## Managing a Kubernetes cluster   
   
Setting up a cluster in EKS is relatively complicated and comes with some prerequisites. You need to set up and use the AWS CLI and aws-iam-authenticator, and set up IAM permissions and users which adds to your workload.   
   
EKS doesn’t create worker nodes automatically, so you’re also in charge of managing that process. You also need to make extra effort to set up EKS with CloudFormation or Terraform.   
   
   
- EKS comes with a **well-defined way of upgrading the control plane with minimized disruption**. You can then update worker nodes using the newer Kubernetes AMI, create a new worker group, and finally migrate your workload to the new nodes.   
- **Scaling up the cluster is simple** and based on adding more worker nodes. The control plane is fully managed, so there’s no need to worry about adding or upgrading master node sizes when your cluster grows.   
- **Carrying out the most common maintenance tasks** is easy in EKS – you can add worker nodes, replace them, terminate instances, and upgrade your setup with minimal disruption to your cluster.   
   
Via - [AWS EKS vs. ECS vs. Fargate vs. Kops: Where to Manage Your Kubernetes in 2022? - CAST AI – Kubernetes Automation Platform](https://cast.ai/blog/aws-eks-vs-ecs-vs-fargate-where-to-manage-your-kubernetes/)   
   
## How does EKS work?   
   
You create a EKS cluster which represents a control plane. These will be master nodes.   
   
When you create an EKS service/cluster AWS will provision Kubernetes master nodes that already have Kubernetes master services installed on them.   
   
Since they're managed by AWS EKS, it'll automatically replicate the master nodes across multiple Availability Zones.   
   
Etcd is part of the master nodes which store the whole configuration/the current state of Kubernetes cluster. This storage is also replicated/backed up by AWS.   
   
For Worker Nodes:   
   
You'll create [aws.EC2](../devlog/aws.EC2.md) instances, so called "Compute Fleet" of multiple virtual servers and connect them to EKS.   
   
Worker nodes have Kubernetes process running on it so the Kubernetes master node can communicate with them.   
   
In this case also, you need to manage the EC2 instance for your worker nodes, yourself.   
   
You have the option of "semi-managed" EC2 instances for your cluster. EKS with Nodegroup. The Nodegroup will handle some of the heavy lifting for you. Basically make it easier for you to configure new worker nodes for your cluster.   
For example: Worker nodes managed by nodegroup will get all the processes necessary installed on them(like container runtime, K8s processes) transform them into Worker Nodes.   
   
It is a good practice to use Nodegroups.   
   
You still need to configure things like [AWS ASG](../devlog/AWS%20ASG.md). Even this can be delegated to AWS you can again combine [AWS Fargate](../devlog/AWS%20Fargate.md) for your EKS cluster.   
   
Fully managed worker nodes with Fargate and Fully managed control plane(master nodes) with EKS.   
   
You can also use EC2 and Fargate in the same EKS cluster.   
   
## Setting up EKS Cluster   
   
   
- Master nodes   
  - Provision an EKS cluster   
- Worker nodes   
  - Create Nodegroup of EC2 instances(compute fleet)   
  - OR you can use Fargate   
- Connect Nodegroup with EKS cluster   
- Connect to cluster using `kubectl`   
  - Deploy your containerized applications   
   
## Labs   
   
   
- [aws.eks.Create EKS cluster with AWS Management Console](../devlog/aws.eks.Create%20EKS%20cluster%20with%20AWS%20Management%20Console.md)   
- [aws.eks.Create EKS cluster with eksctl](../devlog/aws.eks.Create%20EKS%20cluster%20with%20eksctl.md)   
- [aws.eks.Create EKS Cluster with Fargate](../devlog/aws.eks.Create%20EKS%20Cluster%20with%20Fargate.md)   
- [aws.eks.Deploy to EKS Cluster from Jenkins](../devlog/aws.eks.Deploy%20to%20EKS%20Cluster%20from%20Jenkins.md)   
- [aws.eks.Deploy to LKE Cluster from Jenkins](../devlog/aws.eks.Deploy%20to%20LKE%20Cluster%20from%20Jenkins.md)   
- [aws.eks.Complete CI⁄CD Pipeline with EKS and DockerHub](../devlog/aws.eks.Complete%20CI%E2%81%84CD%20Pipeline%20with%20EKS%20and%20DockerHub.md)   
- [aws.eks.Complete CI⁄CD Pipeline with EKS and ECR](../devlog/aws.eks.Complete%20CI%E2%81%84CD%20Pipeline%20with%20EKS%20and%20ECR.md)   
   
## Resources   
   
   
- [EKS Best Practices Guides](https://aws.github.io/aws-eks-best-practices/)