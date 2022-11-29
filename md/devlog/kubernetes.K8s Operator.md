---
created: 1662127348162
desc: ''
id: 0lw4s8f9z8f9a2qiydk6et7
title: K8s Operator
updated: 1662127348162
---
   
**Overview**   
   
Operators are mainly used for stateful applications.    
   
**Stateless applications**   
   
Once deployed, stateless applications don’t need to be controlled, backed up etc. When you carry out some changes, it updates/scales seamlessly. K8s takes care of the heavy lifting using the control loop mechanism of checking desired state with the current state and you always end up with what you wanted.   
   
It doesn’t require business logic to create, update, delete and maintain these applications.   
   
**Stateful  Application Deployment Without Operator**   
   
Let’s say you need a DB for data persistence in your application, these kind of applications require more “hand-holding” throughout the lifecycle.  They require manual intervention.   
   
For example: 3 replicas of a MySQL applications/Pods - aren’t entirely “replicas” they’re not identical. Each has it’s own state and identity. This complicates things such as: updating, deleting them in a certain order. The constant data synchronization needs to be maintained for data consistencies.    
   
These details vary from application to application.   
   
An easier way to manage stateful applications would be to use Operators.   
   
**Stateful Applications With Operator**   
   
They essentially replace human “operators” with software operators.   
   
Manual tasks that a DevOps engineer would do to maintain a stateful application can be handed off to a software operator.   
   
   
- Deploying the applications    
- Creating cluster of replicas    
- Recovery   
   
Tasks are automated and are reusable. 1 standard automated process for different environments.   
   
At it’s core, it has the same Control Loop mechanism that Kubernetes has, that watches for changes in the application state. Did a Pod die? Recreates a new one. Did an application configuration change? Applies the up to date configuration. Did an application image version get bumped? Restarts it with the new image version.   
   
It is a custom control loop.   
   
It uses **CRD**’s = **Custom Resource Definitions**   
   
It is a custom Kubernetes component that extends K8s API. Its like creating a new component on top of the default components.   
   
It also implements domain/application specific knowledge to automate entire lifecycle of the app it operates.   
   
## Who creates the Operators?   
   
They’re created by people who are experts in the business logic of installing, running, updating those specific applications.   
   
Domain specific knowledge people create operator that contains the knowledge of creating a Cluster, how to run it, synchronize data, update. This entire package can be called as an Operator.   
   
Check [OperatorHub.io | The registry for Kubernetes Operators](https://operatorhub.io/)   
   
There’s also Operator SDK that allows developers to create Operators themselves.