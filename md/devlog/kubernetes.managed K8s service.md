---
created: 1662074083264
desc: ''
id: skze3mieblzkou2k5qqj6qf
title: Managed K8s Service
updated: 1662074083263
---
   
Running Kubernetes on the cloud and benefits of using managed Kubernetes service.   
   
**Manaqged VS Unmanaged** K8s Cluster   
   
For an Unmanaged K8s Cluster on a cloud, let's say Linode:   
   
   
- You'd need to spin up some servers for Master nodes.   
- Install master processes on it.   
- Spin up some servers for worker nodes, install `kubectl`, `kube-proxy` and container runtime.   
- You've a cluster but there are many things that you'll need to manually do like back ups, security etc.   
- This can get time consuming, difficult and slow.   
   
For a Managed K8s Cluster on a cloud, let's say LKE(Linode Kubernetes Engine)   
   
   
- You don't have to create cluster from scratch.   
- Most of the set up is done by Linode.   
- You choose how many worker nodes you want.   
- Master Nodes(Control Plane) is created and managed by Cloud Provider in background.   
- The number of responsibilities on you are less, you only pay for Worker Nodes.    
- Less effort and time.