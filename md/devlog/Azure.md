---
category: '2022'
created: 2022-12-05 16:58:38.906000+00:00
id: f0aa9e9c-a8d4-408f-ae4c-ced37d8926d8
tags:
- devlog
title: Azure
updated: 2022-12-05 16:58:39.970000+00:00
---
   
Topics:: [Cloud](../devlog/cloud.md)   
   
   
---   
   
## Azure Portal   
   
> [!info]    
> [Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/intro-to-azure-fundamentals/what-is-microsoft-azure): "The Azure portal is a web-based, unified console that provides an alternative to command-line tools. With the Azure portal, you can manage your Azure subscription by using a graphical user interface."   
   
## Azure Marketplace   
   
> [!info]    
> [Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/intro-to-azure-fundamentals/what-is-microsoft-azure): "Azure marketplace helps connect users with Microsoft partners, independent software vendors, and startups that are offering their solutions and services, which are optimized to run on Azure."   
   
## Availability sets and Availability zones   
   
An availability set is a logical grouping of VMs that allows Azure to understand how your application is built to provide redundancy and availability. It is recommended that two or more VMs are created within an availability set to provide for a highly available application and to meet the 99.95% Azure SLA.   
   
Azure availability zones are **physically and logically separated datacenters with their own independent power source, network, and cooling**. Connected with an extremely low-latency network, they become a building block to delivering high availability applications.   
   
## Azure Policy   
   
Azure Policy is a service in Azure that allows organizations to enforce rules and standards for their Azure resources. It helps ensure that resources are compliant with corporate standards and service level agreements, and helps prevent accidental or unauthorized changes to resources. Azure Policy allows organizations to define policies that can be applied to all or a subset of their Azure resources, and to monitor and report on compliance with those policies. This helps organizations maintain control over their Azure environment and ensures that resources are being used in a consistent and predictable manner.   
   
   
- [Azure Resource Manager](../devlog/Azure%20Resource%20Manager.md)   
- [Azure Managed Disks](../devlog/Azure%20Managed%20Disks.md)   
- [Azure Resource Group](../devlog/Azure%20Resource%20Group.md)    
- [Azure Virtual Machines](../devlog/Azure%20Virtual%20Machines.md)    
- [Azure Batch](../devlog/Azure%20Batch.md)    
- [Azure Service Fabric](../devlog/Azure%20Service%20Fabric.md)    
- [Azure Container Instances](../devlog/Azure%20Container%20Instances.md)   
- [Azure Virtual Machine Scale Sets](../devlog/Azure%20Virtual%20Machine%20Scale%20Sets.md)   
- [Azure Functions](../devlog/Azure%20Functions.md)   
- [Durable Azure Functions](../devlog/Durable%20Azure%20Functions.md)   
- [Azure Kubernetes Service](../devlog/Azure%20Kubernetes%20Service.md)   
- [Azure Storage](../devlog/Azure%20Storage.md)   
- [Azure Subscription](../devlog/Azure%20Subscription.md)   
   
## Networking   
   
   
- **Azure Virtual Network**: Azure Virtual Network allows users to create and manage virtual networks in the cloud. It provides a way to connect Azure resources, such as VMs, to each other and to the internet. Azure Virtual Network also provides features such as security groups and network security groups to help users secure their networks.   
- **Azure Load Balancer**: Azure Load Balancer allows users to distribute incoming traffic across multiple VMs or other resources. It provides a way to evenly distribute traffic and to improve the availability and performance of applications. Azure Load Balancer also provides features such as health probes and automatic failover to help users manage their workloads.   
- **Azure Application Gateway**: Azure Application Gateway is a web traffic load balancer that allows users to manage and distribute incoming traffic to their web applications. It provides features such as SSL termination and URL-based routing to help users manage and secure their web traffic.   
- **Azure ExpressRoute**: Azure ExpressRoute is a dedicated, private connection between Azure and an on-premises network. It allows users to securely connect their on-premises resources to Azure, providing a high-bandwidth and low-latency connection. Azure ExpressRoute also provides features such as redundant connections and built-in disaster recovery to help users ensure the reliability of their connections.   
   
   
- [Azure region](../devlog/Azure%20region.md)   
- [VNet peering](../devlog/VNet%20peering.md)   
   
   
## Security   
   
   
- [Azure Security Center](../devlog/Azure%20Security%20Center.md)    
- [Azure Active Directory](../devlog/Azure%20Active%20Directory.md)    
- [Azure Advanced Threat Protection](../devlog/Azure%20Advanced%20Threat%20Protection.md)    
- [Azure Site Recovery](../devlog/Azure%20Site%20Recovery.md)   
- [Azure Advisor](../devlog/Azure%20Advisor.md)   
- [health probes in Azure](../devlog/health%20probes%20in%20Azure.md)   
   
## Resources   
   
   
- [Azure Fundamentals [AZ-900] Bootcamp (21 Labs & 57 Exercises) - YouTube](https://youtu.be/KzTEJ_hen3c)   
   
## Labs   
   
1.  Create an Azure account and sign in to the Azure portal. Explore the different services and resources available in Azure, and familiarize yourself with the Azure portal interface.   
2.  Create a virtual machine in Azure, and connect to it using Remote Desktop Protocol (RDP). Install some software on the virtual machine, and experiment with configuring the virtual machine's settings and properties.   
3.  Create a storage account in Azure, and upload some files to it using the Azure portal or Azure Storage Explorer. Experiment with configuring the storage account's settings and properties, such as access tiers and replication options.   
4.  Create a web app in Azure, and deploy a web application to it. Configure the web app's settings and properties, such as deployment slots and scaling options. Test the web app by accessing it from a web browser.   
5.  Create a virtual network in Azure, and create some virtual machines and other resources in the virtual network. Experiment with configuring the virtual network's settings and properties, such as subnets and network security groups.   
6. Create a database in Azure, and connect to it using a database management tool. Create some tables, insert some data, and run some queries to retrieve the data. Experiment with configuring the database's settings and properties, such as performance tiers and backup options.   
7.  Create a container in Azure Container Instances, and deploy a container image to it. Test the container by accessing it using its public IP address or DNS name. Experiment with configuring the container's settings and properties, such as resource limits and environment variables.   
8.  Create an Azure Function, and write a function that performs a specific task, such as processing data or sending an email. Test the function by triggering it and verifying the output. Experiment with configuring the function's settings and properties, such as triggers and bindings.   
9.  Create an Azure Load Balancer, and add some virtual machines as backend pool members. Test the load balancer by accessing the virtual machines using the load balancer's public IP address. Experiment with configuring the load balancer's settings and properties, such as health probes and load-balancing rules.   
10.  Create an Azure Logic App, and design a workflow that automates a specific business process, such as data synchronization or approval. Test the logic app by triggering it and verifying the output. Experiment with configuring the logic app's settings and properties   
11. Create an Azure Key Vault, and store some secrets in it. Retrieve the secrets from the key vault, and use them to authenticate to an Azure resource, such as a virtual machine or a database. Experiment with configuring the key vault's settings and properties, such as access policies and network isolation.   
12.  Create an Azure Event Hub, and send some events to it using a producer application. Receive the events from the event hub using a consumer application, and process the events. Experiment with configuring the event hub's settings and properties, such as partitions and consumer groups.   
13.  Create an Azure Stream Analytics job, and design a streaming query that processes data from an Azure Event Hub or IoT Hub. Test the stream analytics job by sending some data to the input and verifying the output. Experiment with configuring the stream analytics job's settings and properties, such as windows and functions.   
14.  Create an Azure Service Bus, and create a queue or a topic in the service bus. Send some messages to the queue or topic using a producer application, and receive the messages using a consumer application. Experiment with configuring the service bus's settings and properties, such as sessions and subscriptions.   
15.  Create an Azure Notification Hub, and register some devices to receive notifications. Send some notifications to the notification hub, and verify