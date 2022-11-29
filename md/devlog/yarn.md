---
created: 20211123165259030
desc: ''
id: 6k7g4x7ws565lditv1n8hxm
title: YARN
updated: 1653318670586
---
   
Topics::  [Big Data](../devlog/big%20data.md)   
   
**Y**et **A**nother **R**esource **N**egotiator   
   
   
- YARN is the main job scheduler and resource allocator for the entire [hadoop](../devlog/hadoop.md) cluster. User applications request resoruces from YARN(contains with data locality).   
- Resources can include cores, memory, GPUs, software licenses and data.   
- Suppose you've a cluster of 10 machines and 50 users and they want to use certain amount of cores and other resources in general, YARN will setup a queue and depending on the policy on the site, jobs get submitted to the queue and YARN will determine when they'll run based on the policy and availability of resources.   
- Each user application is managed at run-time by an ApplicationMaster (AM) container and is responsible for requesting further containers for jobs that are part of the application.   
- AM is basically a localised resource manager for the application that can adapt at run-time for the resources as available.   
- AM manages dynamic resource allocation at run-time. In other words, the **number of mapper processes is usually the number of reducers**.   
- From the cluster view: there is one main ResourceManager and multiple NodeManagers.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.0nif9dneaz0n.png)