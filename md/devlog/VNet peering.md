---
category: '2022'
created: 2022-12-05 19:03:14.018000+00:00
id: 0c9e9a29-7d57-4469-b6d9-c0b8623ea322
tags:
- devlog
title: VNet Peering
updated: 2022-12-05 19:03:14.658000+00:00
---
   
Topics:: [Azure](../devlog/Azure.md)   
   
   
---   
VNet peering is a feature in Azure that allows you to connect two Azure virtual networks (VNets) together, using a direct and private link. This allows resources in the two VNets to communicate with each other, using their private IP addresses, without having to go through the public internet.   
   
VNet peering is useful in a number of scenarios, such as:   
   
   
-   Connecting VNets in different Azure regions, to allow resources in one region to communicate with resources in another region without going through the public internet.   
-   Connecting VNets in different subscriptions, to allow resources in one subscription to communicate with resources in another subscription without going through the public internet.   
-   Connecting VNets in different tenants, to allow resources in one tenant to communicate with resources in another tenant without going through the public internet.