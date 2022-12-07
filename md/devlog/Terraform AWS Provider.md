---
category: '2022'
created: 2022-12-02 21:01:39.654000+00:00
id: bc486e32-1343-49e4-9c06-671bdfae539e
tags:
- devlog
title: Terraform AWS Provider
updated: 2022-12-02 21:01:40.158000+00:00
---
   
Topics:: [Terraform](../devlog/terraform.md)   
   
   
---   
   
[AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)   
   
```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

# Create a VPC
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"
}
```
