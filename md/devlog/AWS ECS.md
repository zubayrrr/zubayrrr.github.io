---
created: 1655534024666
desc: ''
id: y43l1e8ej1au0hfrdkqmdh7
title: AWS ECS
updated: 1656160995036
---
   
Amazon Elastic Container Service (ECS) is a cloud-based and fully-managed container orchestration service. It lets you run your applications in the cloud without having to configure and maintain the infrastructure.   
   
To ensure capacity demands are optimally met and maintain peak performance, you can set ECS to continuously evaluate and monitor memory and CPU processes. This data can help you determine an optimal deployment strategy for each container. Additionally, you can leverage ECS to scale containers and release updates as needed.   
   
ECS supports integration with several useful AWS services and features, including Identity and Access Management ([aws.IAM](../devlog/aws.IAM.md)) roles, Elastic Block Store ([AWS EBS](../devlog/AWS%20EBS.md)) volumes, and AWS Elastic Load Balancing ([AWS ELB](../devlog/AWS%20ELB.md)).   
   
It manages the entire lifecycle of a container, whether you need to spin some up, reschedule, restart, load balance. It has got you covered.   
   
## ECS Cluster   
   
To get started you need to create an ECS cluster. That will contain all the services that are needed to manage the individual containers.   
   
ECS Cluster basically represents a control plane for all your virtual machines running containers.   
   
The containers need to run on actual machines...these virtual machines will be [aws.EC2](../devlog/aws.EC2.md) instances. ECS Cluster is just providing a "Control Plane" for managing all of this.   
   
The EC2 instance created will not isolated but it'll be connected and managed by the Control Plane processes installed on ECS Cluster that we created.   
   
   
- Those EC2 instances will have [docker](../devlog/docker.md)/container runtime so that containers can run.   
- They'll also have ECS agents installed so they can communicate with each EC2 instance and manage them.   
   
**Pros:**   
   
You have full control over the type of EC2 instance used here. For example, you can use a GPU-optimized instance type if you need to run training for a machine learning model that comes with unique GPU requirements.   
You can take advantage of spot instances that reduce cloud costs by up to 90%.   
   
**Cons:**   
   
You’re the one responsible for security patches and network security of the instances, as well as their scalability in the cluster (but thankfully, you can use Kubernetes autoscaling for that).   
   
You'd still need to manage the EC2 instances like creating them, joining them with your ECS cluster, when a new container is scheduled; you have to make sure that you've enough resources for it). You also have to manage the server's OS, updates, patches etc. So the only pain is managing the virtual machines themselves.   
   
**Cost:** You’re charged for the EC2 instances run within your cluster and VPC networking.   
   
See: [AWS Fargate](../devlog/AWS%20Fargate.md)   
   
## Resources   
   
   
- [AWS ECS in Depth: Architecture and Deployment Options](https://cloud.netapp.com/blog/aws-cvo-blg-aws-ecs-in-depth-architecture-and-deployment-options)