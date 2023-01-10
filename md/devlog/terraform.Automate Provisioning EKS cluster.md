---
created: 1661426504332
desc: ''
id: xq7qktjqyrecaa9plxpck9c
title: Automate Provisioning EKS cluster
updated: 1661434070783
---
   
Topics::  [kubernetes](../devlog/kubernetes.md), [terraform](../devlog/terraform.md), [aws.eks](../devlog/aws.EKS.md)   
   
   
---   
   
We've seen [aws.eks.Create EKS cluster with AWS Management Console](../devlog/aws.eks.Create%20EKS%20cluster%20with%20AWS%20Management%20Console.md) and [aws.eks.Create EKS cluster with eksctl](../devlog/aws.eks.Create%20EKS%20cluster%20with%20eksctl.md), both of these setups had a lot of moving parts. They don't have any version control, team collaboration is difficult, no simple replication of infrastructure is possible and no simple clean up.   
   
We can instead use [terraform](../devlog/terraform.md) to achieved this, which is a lot more streamlined and modular. Terraform is currently the best way to provision an EKS cluster!   
   
**Overview/Steps**   
   
   
- Control Plane that is managed by AWS, the actual EKS service.   
- Create worker nodes and connect them to master node.   
  - Create a VPC   
  - Create worker nodes(EC2 instances or Node Group)   
- Choosing the region for the cluster.   
   
The complete Terraform code can be found at [feature/eks](https://gitlab.com/zubayrrr/terraform-learn/-/tree/feature/eks)   
   
**VPC**   
   
EkS needs very specific configuration of VPC and the subnet inside and the route tables. We can refer to a [aws.cloudformation](../devlog/aws.CloudFormation.md) template for achieving this.   
   
Using Terraform Module for VPC.   
   
```tf
provider "aws" {
    region = "eu-west-2"
}

variable vpc_cidr_block {}
variable private_subnet_cidr_blocks {}
variable public_subnet_cidr_blocks {}

data "aws_availability_zones" "available" {}


module "myapp-vpc" {
    source = "terraform-aws-modules/vpc/aws"
    # modules are also packages of code that we need to download when we want to use them. Downloaded on `terraform init`
    version = "2.64.0"

    # 14 attributes/variables are needed to be defined for creating a VPC

    name = "myapp-vpc"
    cidr = var.vpc_cidr_block
    # best practice 1 private 1 public subnet in each AZ
    private_subnets = var.private_subnet_cidr_blocks
    public_subnets = var.public_subnet_cidr_blocks
    azs = data.aws_availability_zones.available.names # dynamically set AZs, using data to query

    enable_nat_gateway = true # default = one NAT gateway per subnet
    single_nat_gateway = true # all private subnets will route their internet traffic through single NAT gatway
    enable_dns_hostnames = true

    tags = {
        "kubernetes.io/cluster/myapp-eks-cluster" = "shared"
        # to label what env they belong to etc, for human consumption, to have more information. It can also be used for referencing programmatically from other components e.g Cloud Controller Manager

        # for telling CCM, which resource to talk to, which VPC should be used, what subnets should be used.
    }

    public_subnet_tags = {
      # for load balancer, open for external request, resources provisioned that has external IP address must be deployed here.
        "kubernetes.io/cluster/myapp-eks-cluster" = "shared"
        "kubernetes.io/role/elb" = 1
    }

    private_subnet_tags = {
      # for internal load balancer
        "kubernetes.io/cluster/myapp-eks-cluster" = "shared"
        "kubernetes.io/role/internal-elb" = 1
    }

}
```
   
   
**EKS Cluster**   
   
Using the Terraform Module for EKS.   
   
```tf
provider "kubernetes"{
  load_config_file = "false"
  host = data.aws_eks_cluster.myapp-cluster.endpoint # endpoint of K8s cluster(API Server)
  token = data.aws_eks_cluster_auth.myapp-cluster.token
  cluster_ca_certificate =  base64decode(data.aws_eks_cluster.myapp-cluster.certificate_authority.0.data)
}

data "aws_eks_cluster" "myapp-cluster" {
  name = module.eks.cluster_id
}

data "aws_eks_cluster_auth" "myapp-cluster" {
  name = module.eks.cluster_id
}

module "eks" {
  source  = "terraform-aws-modules/eks/aws"
  version = "18.21.0"

  cluster_name = "myapp-eks-cluster"
  cluster_version = "1.22"

  subnet_ids = module.myapp-vpc.private_subnets # our workload, public is for external resources like load balancers.
  vpc_id = module.myapp-vpc.vpc_id

  tags = {
    environment = "development"
    application = "myapp"
  }

  eks_managed_node_groups = {
    dev = {
      min_size     = 1
      max_size     = 3
      desired_size = 3

      instance_types = ["t2.small"]
    }
  }
}
```
   
   
**Authenticate with K8s cluster**   
   
Configure the [kubernetes](../devlog/kubernetes.md) provider.   
   
**Deploy ngnix-App into our cluster**   
   
   
- Configure `kubectl` with cluster kubeconfig file.   
  - A default file is created when you run `kubectl` for the first time inside the user's home dir `~/.kube/config`   
  - This file contains all the information about the cluster like its endpoint, CA certificate, token, IAM authenticator.   
- [aws cli](../devlog/aws%20cli.md), `kubectl` and `aws-iam-authenticator` must be installed.   
   
`aws eks update-kubeconfig --name myapp-eks-cluster --region eu-west-2` to add a new context to `~/.kube/config`.   
   
   
`kubectl get node` will list all the worker nodes.   
   
`kubectl get pod` will list whats been deployed.   
   
lets deploy a simple application.   
   
`kubectl apply -f ~/Documents/ngnix-config.yaml`   
   
`kubectl get svc` to list services   
   
   
**Destroy all components**   
   
`terraform destroy`   
`terraform state list`   
   
See also: [ansible.Deploying Application in K8s](../devlog/ansible.Deploying%20Application%20in%20K8s.md)