---
category: '2022'
created: 2022-12-05 17:06:32.230000+00:00
id: 25eaf276-5e81-48de-a60b-3d30bc5174d7
tags:
- devlog
title: Azure Resource Manager
updated: 2022-12-05 17:06:32.934000+00:00
---
   
Topics:: [Azure](../devlog/Azure.md)   
   
   
---   
   
> [!info]    
> [Azure docs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview): "Azure Resource Manager is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources in your Azure account. You use management features, like access control, locks, and tags, to secure and organize your resources after deployment."   
   
The Azure Resource Manager (ARM) is a service in Microsoft Azure that provides a consistent management layer for deploying, managing, and monitoring Azure resources. ARM allows you to create, update, and delete resources in Azure, as well as manage their dependencies and relationships.   
   
ARM templates are JSON-based files that define the infrastructure and configuration of an Azure solution. These templates are used to deploy and manage Azure resources, such as virtual machines, storage accounts, and virtual networks. The templates follow a specific format, which includes a list of parameters, variables, and resources.   
   
The format for ARM templates includes the following elements:   
   
   
-   Parameters: These are values that are provided at deployment time and are used to customize the deployment.   
-   Variables: These are values that are defined within the template and can be used throughout the template.   
-   Resources: These are the Azure resources that are deployed and managed by the template. This includes the type of resource, its properties, and its dependencies on other resources.   
-   Outputs: These are values that are returned by the template after deployment, such as the URL of a web app or the ID of a virtual machine.   
   
An example of an ARM template might look like this:   
   
```json
{
"$schema":"https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
   "contentVersion":"1.0.0.0",
   "parameters":{
      "vmName":{
         "type":"string",
         "defaultValue":"myVM"
      },
      "vmSize":{
         "type":"string",
         "defaultValue":"Standard_D1_v2"
      }
   },
   "variables":{
      "location":"[resourceGroup().location]",
      "osDiskName":"[concat(parameters('vmName'), '_OSDisk')]"
   },
   "resources":[
      {
         "type":"Microsoft.Compute/virtualMachines",
         "apiVersion":"2019-03-01",
         "name":"[parameters('vmName')]",
         "location":"[variables('location')]",
         "properties":{
            "hardwareProfile":{
               "vmSize":"[parameters('vmSize')]"
            },
            "osProfile":{
               "computerName":"[parameters('vmName')]",
               "adminUsername":"adminuser",
               "adminPassword":"P@ssw0rd!"
            },
            "storageProfile":{
               "osDisk":{
                  "createOption":"fromImage",
                  "name":"[variables('osDiskName')]"
               }
            },
            "networkProfile":{
               "networkInterfaces":[
                  {
                     "id":"[resourceId('Microsoft.Network/networkInterfaces', concat(parameters('vmName'), '_NIC'))]"
                  }
               ]
            }
         }
      }
   ]
}
```
