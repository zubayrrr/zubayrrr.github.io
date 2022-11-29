---
created: 1662060199372
desc: Deploying Stateful Applications
id: p7hfnq5543ukh0qlnwwnxfx
title: StatefulSet
updated: 1662060199372
---
   
StatefulSet is a Kubernetes component that is used specifically for stateful applications.   
   
Example of stateful applications:   
   
   
- Databases   
- Any application that stores data to keep track of it’s state.   
   
Sometimes stateless applications connect to stateful applications to forward requests.   
   
Stateless applications are deployed using **Deployment** component, where Deployment is an abstraction of Pods and allows you to replicate that stateless application(run identical pods)  in the cluster.   
   
Stateful applications are deployed using **StatefulSet** component. Just like Deployment, StatefulSet does allow you to replicate the stateful application/Pods.   
   
**Both Deployment and StatefulSet manage Pods based on container specification.** Configuring the storage for both of them is same.   
   
So what’s the difference between Deployment and StatefulSet?   
   
   
- Replicating stateful applications is more difficult compared to stateless application and has additional requirements.   
   
StatefulSet Pod’s replica Pods are not identical, in fact they each have their own additional identity, on top of the common blueprint of the Pod that they get created from.   
   
StatefulSet:   
   
   
- Maintains sticky identity for each Pod.   
- Created from same specification but are not interchangeable.   
- Each Pod has a persistent identifier that it maintains across any re-scheduling(rebirth).   
   
Why do these Pods need identity and why are they not interchangeable?   
   
**Scaling DB applications**   
   
If you allow two independent instances of a DB application to change the same data, you’ll get data inconsistencies. So there is a mechanism that allows only one Pod to change data which is shared. Reads by multiple Pods is fine. Pod that is allowed to update data is called Master others are called Slaves/Worker.   
   
Pods don’t have access to the same physical storage even though they use the same data, they don’t use the same physical storage. Each has their own replicas of storage that each one of them accept for itself. Each pod replica at any time must have the same data  as the other ones.  They’ve to continuously synchronise the data.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662070018/wiki/dkcvku99b1fujjk19p4o.png)   
   
   
The slaves/workers must know about each change for them to be up to date with the Master.   
   
When a new replica Pod joins an existing set up, the new Pod needs to create it’s own storage and sync. It first clones the data from the previous Pod(not just any Pod) and then starts syncing.   
   
Theoretically, temporary storage is possible if Pods just keep replicating data from each other. But if the cluster crashes or all Pods die at the same time. They data will be lost forever.  It is a best practice to use data persistence for stateful applications.   
   
With persistent storage, data will survive even if all Pods die or even if you delete the complete StatefulSet component because PV lifecycle isn’t tied to the other component’s lifecycle.   
   
**Configuring persistent volume for StatefulSet**   
   
Since each Pod has it’s own data storage(PV backed up by it’s own physical storage). Pod’s state is also stored on Pod’s own storage. When a Pod dies and is reborn, the persistent Pod identifiers makes sure the storage volume gets reattached. For this re-attachment to work, its important to use remote storage. Because if the Pod gets rescheduled from one Node to another Node the previous storage must be available on the other Node as well(cannot be done local volume storage because they’re usually tied to a specific node).   
   
**Pod identifier**   
   
StatefulSet Pods each have a Pod identifier, unlike Deployment Pods that get random hashes at the end in their name. StatefulSet Pods get fixed ordered names which is `$(statefulSet name)-$(ordinal)`, the `0th` ordinal is the Master and the subsequent Pods are slaves in the order of the ordinal.    
   
StatefulSet will not create the next Pod and the replica if the previous one isn’t already up and running, the deletion works in the reverse order.   
   
**2 Pod endpoints**   
   
Each Pod in a StatefulSet gets its own DNS endpoint from a service.   
   
Service name for stateful application (just like for Deployment) that will address any replica Pods, additionally individual DNS (service) name for each Pod.   
   
The individual DNS names are made up of `${pod name}.${governing service name}` which is a service name that you define inside the StatefulSet.   
   
1. predictable Pod Name   
2. fixed individual DNS name   
   
When a Pod restarts:   
   
   
- IP address changes but   
- name and endpoint stays same.    
   
Sticky identity makes sure the Pod after restart retains state and retains role.   
   
   
**Replicating stateful apps**   
   
Stateful applications are not perfect candidates for containerized environments which is why even though Kubernetes does a lot of the work, theres still a lot of manual configuring that you have to take care of.   
   
   
- configuring the cloning and data synchronization.   
- make remote storage available.   
- managing and back up.