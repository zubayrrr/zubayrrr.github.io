---
created: 20211122182350620
desc: ''
id: llkslspv5gn64h1n4w6hzuc
title: Spark Cluster Managers
updated: 1653305218724
---
   
Topics::  [apache spark](../topics/apache%20spark.md)   
   
   
---   
   
### Spark Standalone mode   
   
   
- By default applications submitted to the standalone mode cluster will run in FIFO order and each application will try to use all available nodes.   
- Which basically means you'll have multiple nodes and you'd have one master node running and the other nodes will be Spark Worker processes running.   
- It'll not be a distributed file system since it is a standalone mode, it'll rely on external sources to get data or the file system of the node where the data is stored. (the processes will happen across the worker nodes)   
   
### Apache Mesos   
   
   
- Apache Mesos is an open-source project to manage computer clusters and can also run [hadoop](../devlog/hadoop.md) applications.   
   
### hadoop YARN/Apache YARN   
   
   
- Apache YARN is the cluster resource manager of hadoop 2.   
- Spark can run on YARN.   
   
### Kubernetes   
   
   
- Kubernetes is an open-source system for automating, deployment, scaling and management of containerized applications.