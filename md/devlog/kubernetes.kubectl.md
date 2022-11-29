---
created: 1661601061024
desc: ''
id: ksyhghr3epi21n0q3otj46t
title: Kubectl
updated: 1661601064770
---
   
`Kubectl` is the Kubernetes command line tool that allows you to run commands against Kubernetes clusters. For example, you can use it to create, delete, list, and inspect Kubernetes objects. It is basically a client for the Kubernetes API Server.   
   
   
- Get all components   
   
`kubectl get all`   
`kubectl get all | grep`   
   
   
- Get status of nodes   
   
`kubectl get nodes`   
   
   
- Get status of pods   
   
`kubectl get pods`   
   
   
- Get status of services   
   
`kubectl get services`   
   
   
- Create components   
   
`kubectl create`   
   
   
- Create deployment   
   
`kubectl create deployment nginx-depl --image=nginx` (most basic blueprint, rest are defaults)   
   
   
- Get deployments   
   
`kubectl get deployment`   
   
   
- Replicaset - managing replicas of a pod   
   
`kubectl get replicaset`   
   
   
- Edit deployment   
   
`kubectl edit deployment nginx-depl` (will get auto-generated config file with default values)   
   
### Debugging pods   
   
`kubectl logs pod-name`   
   
   
- Get additional information about a pod   
   
`kubectl describe pod pod-name`   
   
   
- Get the terminal of the application(pod)   
   
`kubectl exec -it pod-name -- bin/bash`   
   
   
- Delete deployment   
   
`kubectl delete deployment deployment-name`