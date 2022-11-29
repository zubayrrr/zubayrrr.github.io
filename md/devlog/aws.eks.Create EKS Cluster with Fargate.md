---
created: 1662680302898
desc: ''
id: bjnmmrc8u215bwtrc042v53
title: Create EKS Cluster with Fargate
updated: 1662697388030
---
   
Related::  [aws.fargate](../devlog/aws.fargate.md), [kubernetes](../devlog/kubernetes.md)   
   
   
---   
   
We've seen how to run EKS cluster with Node Group(EC2 instances managed by us) in [aws.eks.Create EKS cluster with AWS Management Console](../devlog/aws.eks.Create%20EKS%20cluster%20with%20AWS%20Management%20Console.md).   
   
As an alternative to Node Groups and EC2 instances we can also work with [aws.fargate](../devlog/aws.fargate.md).   
   
We can go full serverless(no EC2 instances on our AWS account) and let AWS managed account create resources.   
   
The difference between EC2 instances and Fargate is that when we create Pods using Fargate, it'll provision it's own virtual machines for each Pod. We'll have as many virtual machines as Pods. On EC2 instances however, we can have as many Pods as we want on a single instance(virtual machine).   
   
This can have limitations on what we can do with Fargate, for example: theres no support for stateful applications or DaemonSets as of yet.   
   
We can have Fargate in addition to Node Group attached to our EKS cluster!   
   
## Create IAM Role for Fargate   
   
When our cluster creates Pods on Fargate; the Pods(kubelet) provisioned on VMs by Fargate on need permissions to calls to AWS API on our behalf. It'll need to connect to our VPC, create resources, pull images from [aws.ecr](../devlog/aws.ecr.md) etc.   
   
We need a Role to provision VMs by Fargate.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662681332/wiki/svqjdg22gjtf8goowwvu.png)   
   
The `AmazonEKSFargatePodExecutionRolePolicy` will be auto selected.   
   
## Create Fargate Profile   
   
“Add Fargate Profile” from EKS Cluster page.   
   
**Configure pod selection**   
   
We tell provide a Deployment to Fargate, based on the profile rules can decide whether that Pod should be scheduled through Fargate.   
   
We can use both Node Group and Fargate for EKS cluster.   
   
Fargate profile lets us define the criteria to decide how a Pod should be scheduled.   
   
**Why do we need to provide our VPC**   
   
The pods that will get scheduled need to have an IP address from our subnet IP range.   
   
**Pod selectors**   
   
We need some type of selector that will tell Fargate this pod is meant to be scheduled using Fargate.   
   
In the Deployment config, under the `metadata` attribute you can define something like `namespace: dev`,   
   
The other option is to use label selector(`matchLabels`). you can add arbitrary key-value pairs as labels and use that as Pod selector rules. They’re kinda like tags.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662682878/wiki/gsv3kbdpqnbuzsgkdqyj.png)   
   
**Use case: having both Node Group and Fargate for our cluster**   
   
   
- We can have both Dev and Test environments inside the same cluster.   
  - We can decide based on namespace or match labels what Pods we want to deploy to Fargate.   
- Fargate has limitations when it comes to what kind of Deployments we can make.   
  - We can go with Node Group for stateful applications and DaemonSets   
  - And Fargate profile for stateless applications.   
   
   
## Deploy Pod through Fargate   
   
![uploading...](31m.0lwa)   
   
**Create Namespace `dev`**   
   
`kubectl create ns dev`   
   
All thats left for us to do is to `apply -f` our application configuration.   
   
`kubectl apply -f ngnix-config.yaml`   
   
`kubectl get pods -n dev`   
   
and since Fargate is completely managed by AWS you will have no access to it’s VMs directly.   
   
and if you reapply the configuration with the `default` Namespace, the cluster will kill the Fargate pods and launch a new Pod in the default NS.   
   
`kubectl get pods -n default -o wide`   
   
## Clean up   
   
To clean up cluster resources and destroy the cluster.   
   
   
- Before we can delete the cluster, we’ll need to delete the Node Group and Fargate Profile.   
- Deleting the cluster may take some time.   
- Delete the IAM Roles that we had created.   
- We need to the CloudFormation Stack as well.   
- The EC2 instances will be killed when you kill the Node Group.