---
category: '2022'
created: 2022-12-05 17:09:43.414000+00:00
id: 05ad1fc4-c06f-45b6-9231-eae0bdcbff22
tags:
- devlog
title: Azure Managed Disks
updated: 2022-12-05 17:09:44.126000+00:00
---
   
Topics:: [Azure](../devlog/Azure.md)   
   
   
---   
Azure managed disks are a type of storage in Microsoft Azure that simplifies the management of virtual machine disks. Instead of managing the disks yourself, Azure manages the disks for you, including the underlying storage infrastructure.   
   
Azure managed disks offer several benefits over unmanaged disks, such as automatic storage provisioning, improved availability, and enhanced security. With managed disks, you don't need to worry about configuring storage accounts, partitions, or data replication. Azure takes care of these tasks for you, so you can focus on deploying and managing your virtual machines.   
   
Managed disks are available in several different types, including standard, premium, and ultra disks. Standard disks are suitable for most workloads and offer balanced performance and capacity. Premium disks are optimized for I/O-intensive workloads, such as databases, and offer high performance and low latency. Ultra disks are the highest performance disks available in Azure, and are suitable for workloads that require extremely low latency and high IOPS.   
   
To use managed disks, you simply specify the disk type and size when you create a virtual machine. Azure automatically provisions the required storage and attaches the disks to the virtual machine. You can then manage the disks through the [Azure Portal](/not_created.md), [Azure CLI](../devlog/Azure%20CLI.md), or [Azure PowerShell](/not_created.md).