---
created: 1661987137854
desc: Persisting Data with Volumes
id: q0yq9ul39z4pml6b2ylvsqb
title: Volumes
updated: 1662328308821
---
   
There are 3 components to Kubernetes storage:   
   
1. Persistent Volume   
2. Persistent Volume Claim   
3. Storage Class   
4. emptyDir   
   
**The need for volumes**   
   
Kubernetes doesn't offer storage out of the box, you've to configure it explicitly for each application that needs saving data before each pod restart.   
   
**Storage requirements**   
   
   
- You need a storage that doesn't depend on pod lifecycle. It'll still be there when a pod takes a rebirth. The new pod will pick up where the previous one left off.   
   
   
- It should be available for all nodes not just one specific one. So all the nodes/pods share the same data.   
   
   
- You need highly available storage, that can survive even if cluster crashes.   
   
**Other use cases** may involve reading/writing to a directory for your application. Session files, application files, configuration files etc.   
   
## Persistent Volume   
   
You can configure any kind of storage needs using persistent volumes.   
   
   
- Think of it as a cluster resource(just like RAM or CPU).   
- It is created using a [languages.YAML](../devlog/languages.YAML.md) file.   
- Since a persistent volume is an abstraction, it actually needs physical storage(local harddrive, NFS server, cloud storage).   
- Where does this storage comes from and who makes it available to the cluster?   
  - Kubernetes doesn’t help you manage storage.   
  - You’ve define what type of storage you need.   
  - Create it and manage it yourself(backing up, recovery etc).   
  - Think of it as an external plugin for your cluster.   
   
**Persistent volume YAML example**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662040183/wiki/ucahcrgsnazvrtoaow3d.png)   
   
Google cloud for storage   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662040296/wiki/mywanihnedt5vgw7gvj1.png)   
   
Depending on storage type, storage backend spec attributes differ.   
   
Local storage   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662040343/wiki/lsmfhwg8xfzpngoy2t17.png)   
   
You can check all the supported type of volumes: [Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/volumes/#volume-types)   
   
Persistent volumes are not namespaced. They’re accessible to the whole cluster.   
   
**Local vs Remote**   
Volume types:   
   
   
- Each volume has its own use case!   
- Local volume types violate the 2 and 3 requirement for data persistence.   
  - Not being tied to one specific node.   
  - Surviving cluster crashes   
- You should almost always use remote storage.   
   
**Who creates persistent volumes and when**   
   
Since storage is like a resource, it needs to exist before a pod that depends on it is created.   
   
## PVCs   
   
They’re also created by YAML config files.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662041023/wiki/kykg18f29jfwhrmvod6l.png)   
   
PVC claims a volume with certain storage size/capacity defined in the YAML file and some additional characteristics. Whatever PV satisfies this claim(matches criteria) will be used for the application.   
   
You will also have to use this claim in your pod configuration so that the pods may have access to those persistent volumes.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662041114/wiki/vien9vzeeddium1qchxx.png)   
   
**Level of Volume Abstractions**   
   
   
- Pod requests the volume through PV claim. Pods access the storage by using the claim as a volume.   
- Claim tries to find a volume in cluster that satisfies the claim.   
- Volume has the actual storage backend.   
- Claims must exist in the same namespace as the pod using the claim.   
- Once the claim finds the PV, it is mounted into the pod.   
- This volume can now be mounted into a container running inside that pod.   
- If you’ve multiple containers, you can choose to mount it on all the containers or just some of them.   
   
**Why so many abstractions**   
   
   
- Admin has to provision storage resource.   
- User creates a claim to PV.   
   
This actually an advantage for the K8s user. They’ve to do less work, they don’t have to worry where the storage is coming from.   
   
**ConfigMap & Secret**   
   
Both ConfigMap and Secret are also a type of volumes. Both of them are local volumes and unlike the other kind of volumes, they’re not created by PV and PVC but rather managed by K8s.   
   
Let’s say you need to a config file for your [prometheus](../devlog/prometheus.md) pod or maybe for a message broker service. OR when you need a certificate file mounted inside your application. In both cases you need a file available for your pod. You can achieve this using either ConfigMap or Secret component. You create them and reference(mount) them in your Pod.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662041723/wiki/tvecjvztnd2yb5bsbrif.png)   
   
**Different volume types in a Pod**   
   
A pod can use multiple volumes of different types simultaneously.   
   
**Storage Class**   
   
Consider a cluster with hundreds of Pod that require storage regularly. Admins will have to manually create the storage.   
   
Storage Class creates PV dynamically. Whenever PVC claims it. It is a way to automate creation of PV.   
   
They’re created by YAML file.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662042275/wiki/tyw6bu6mvxbwtbgfhcr5.png)   
   
Storage backend is defined in SC component via the “provisioner” attribute, each storage backend has it’s own provisioner that K8s offers internally that are prefixed with `"kubernetes.io"`. For other storage types there are external provisioners.   
   
SC is another abstraction level that abstracts underlying storage provider as well as the parameters of the storage.   
   
To use it, it has to be claimed by PVC.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662042560/wiki/l2jrvwrxxpkti5lt4k0z.png)   
   
1. Pod claims storage via PVC.   
2. PVC requests storage from SC.   
3. SC creates PV that meets the needs of the claim using provisioner from the actual storage backend.   
   
**K8s Admin & K8s User**   
   
Admin sets up and maintains the cluster, makes sure the cluster has enough resources(sysadmins, DevOps engineers). Storage resource is provisioned by Admin. They configure the storage(cloud, NFS) and also create the PV components from the storage backends. They do this based on the requirement by the developer teams. Application has to claim the volume storage(this is taken care by K8s User). See PVC.   
   
User deploys applications to the cluster either directly or through CI pipeline(developers).   
   
## emptyDir   
   
It starts off empty, emptyDir volume is created when a Pod that references it starts on a Node. It runs as long as the Pod is running on that specific Node. If the Pod dies and gets rescheduled on another Node, all the data on the emptyDir is deleted permanently and starts with a fresh state on another Node.   
   
If the container crashes and the Pod itself doesn't really die, it doesn't remove the contents of emptyDir, it'll still be there when the container restarts.