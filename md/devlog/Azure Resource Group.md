---
category: '2022'
created: 2022-12-05 16:58:38.906000+00:00
id: e4091518-3879-42f0-a74a-b3c63e8a8cc3
tags:
- devlog
title: Azure
updated: 2022-12-05 17:12:46.678000+00:00
---
   
Topics:: [Azure](../devlog/Azure.md)   
   
   
---   
> [!info]    
> [Azure docs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal): "A resource group is a container that holds related resources for an Azure solution. The resource group can include all the resources for the solution, or only those resources that you want to manage as a group."   
   
An Azure Resource Group is a logical container in Microsoft Azure that allows you to group related Azure resources together. Resource groups make it easier to manage, deploy, and delete your Azure resources, as well as control access to them.   
   
A resource group typically contains all of the resources that are required to run a specific application or service. For example, a resource group might include a virtual machine, a storage account, and a virtual network. This allows you to manage all of these resources as a single unit, rather than managing them individually.   
   
Resource groups also allow you to control access to your Azure resources. You can use Azure Role-Based Access Control (RBAC) to grant users and groups access to a specific resource group, rather than granting access to individual resources. This makes it easier to manage access to your Azure resources and helps to ensure that they are used in accordance with your corporate policies.   
   
To create a resource group, you simply specify a name and a location in Azure. You can then add and remove resources from the resource group as needed. You can manage resource groups through the [Azure Portal](/not_created.md), [Azure CLI](../devlog/Azure%20CLI.md), or [Azure PowerShell](/not_created.md).