---
created: 1653568963869
desc: ''
id: hjm4wdsz5kubm8h8pm006dd
title: Load Balancer
updated: 1656064086045
---
   
What is a Load Balancer? A load balancer acts as the “traffic cop” sitting in front of your servers and routing client requests across all servers capable of fulfilling those requests in a manner that maximizes speed and capacity utilization and ensures that no one server is overworked, which could degrade performance.   
   
If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the server group, the load balancer automatically starts to send requests to it.   
   
## Types of Load Balancers – Based on Functions   
   
Several load balancing techniques are there for addressing the specific network issues:   
   
**Network Load Balancer / Layer 4 (L4) Load Balancer:**   
   
Based on the network variables like [IP address](../devlog/ip%20address.md) and destination ports, Network Load balancing is the distribution of traffic at the transport level through the routing decisions. Such load balancing is TCP i.e. level 4, and does not consider any parameter at the application level like the type of content, cookie data, headers, locations, application behavior etc. Performing network addressing translations without inspecting the content of discrete packets, Network Load Balancing cares only about the network layer information and directs the traffic on this basis only.   
   
**Application Load Balancer / Layer 7 (L7) Load Balancer:**   
   
Ranking highest in the [OSI model](../devlog/osi%20model.md), Layer 7 load balancer distributes the requests based on multiple parameters at the application level. A much wider range of data is evaluated by the L7 load balancer including the HTTP headers and SSL sessions and distributes the server load based on the decision arising from a combination of several variables. This way application load balancers control the server traffic based on the individual usage and behavior.   
   
**Global Server Load Balancer/Multi-site Load Balancer:**   
   
With the increasing number of applications being hosted in cloud data centers, located at varied geographies, the GSLB extends the capabilities of general L4 and L7 across various data centers facilitating the efficient global load distribution, without degrading the experience for end users. In addition to the efficient traffic balancing, multi-site load balancers also help in quick recovery and seamless business operations, in case of server disaster or disaster at any data center, as other data centers at any part of the world can be used for business continuity.   
   
## Types of Load Balancers – Based on Configurations   
   
Load Balancers are also classified as:   
   
**Hardware Load Balancers:**   
   
As the name suggests, this is a physical, on-premise, hardware equipment to distribute the traffic on various servers. Though they are capable of handling a huge volume of traffic but are limited in terms of flexibility, and are also fairly high in prices.   
   
**Software Load Balancers:**   
   
They are the computer applications that need to be installed in the system and function similarly to the hardware load balancers. They are of two kinds- Commercial and Open Source and are a cost-effective alternative to the hardware counterparts.   
   
**Virtual Load Balancers:**   
   
This load balancer is different from both the software and hardware load balancers as it is the combination of the program of a hardware load balancer working on a virtual machine.   
   
Through virtualization, this kind of load balancer imitates the software driven infrastructure. The program application of hardware equipment is executed on a virtual machine to get the traffic redirected accordingly. But such load balancers have similar challenges as of the physical on-premise balancers viz. lack of central management, lesser scalability and much limited automation.   
   
## Load Balancing Methods   
   
All kinds of Load Balancers receive the balancing requests, which are processed in accordance with a pre-configured algorithm.   
   
**Industry Standard Algorithms**   
   
The most common load balancing methodologies include:   
   
   
- Round Robin Algorithm:   
  It relies on a rotation system to sort the traffic when working with servers of equal value. The request is transferred to the first available server and then that server is placed at the bottom of the line.   
   
   
- Weighted Round Robin Algorithm:   
  This algorithm is deployed to balance loads of different servers with different characteristics.   
   
   
- Least Connections Algorithm:   
  In this algorithm, traffic is directed to the server having the least traffic. This helps maintain the optimized performance, especially at peak hours by maintaining a uniform load at all the servers.   
   
   
- Least Response Time Algorithm:   
  This algorithm, like the least connection one, directs traffic to the server with a lower number of active connections and also considers the server having the least response time as its top priority.   
   
   
- IP Hash Algorithm:   
  A fairly simple balancing technique assigns the client’s IP address to a fixed server for optimal performance.   
   
Via - [Load Balancer | Types of Load Balancers | Benefits of Load balancer](https://www.appviewx.com/education-center/load-balancer-and-types/)