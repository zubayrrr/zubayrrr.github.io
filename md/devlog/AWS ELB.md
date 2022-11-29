---
created: 1656063092806
desc: ''
id: uedjwc3ldf8k1p2l1l7fcxj
title: AWS ELB
updated: 1656064060864
---
   
Elastic Load Balancing supports the following types of load balancers: Application Load Balancers, Network Load Balancers, and Classic Load Balancers. Amazon ECS services can use these types of load balancer. Application Load Balancers are used to route HTTP/HTTPS (or Layer 7) traffic. Network Load Balancers and Classic Load Balancers are used to route [TCP](../devlog/TCP.md) (or Layer 4) traffic.   
   
**Classic Load Balancer**   
   
   
- Uses Round Robin traffic routing   
- Will be deprecated from Aug 2022   
   
**Application Load Balancer**   
   
   
- Path based routing - if you have path `/home` or `/mobile` serving different pages from different ASGs.   
- Multiple ASG balancing.   
   
**Network Load Balancer**   
   
   
- Streaming service(packet transmission)   
- Uses network layer (TCP protocol) (makes this LB faster)   
   
**Gateway Load Balancer**   
   
   
- GWLB Target groups support the Generic Networking Virtualization Encapsulation(**GENEVE**) on port: 6081.   
- Runs within one Availability Zone.