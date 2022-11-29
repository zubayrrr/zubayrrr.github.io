---
created: 1661600976214
desc: ''
id: uck8og3odvjj4in3jso008k
title: Namespaces
updated: 1661600984205
---
   
Namespaces are a way to organize clusters into virtual sub-clusters — they can be helpful when different teams or projects share a Kubernetes cluster. Any number of namespaces are supported within a cluster, each logically separated from others but with the ability to communicate with each other. Namespaces cannot be nested within each other.   
   
Any resource that exists within Kubernetes exists either in the default namespace or a namespace that is created by the cluster operator. Only nodes and persistent storage volumes exist outside of the namespace; these low-level resources are always visible to every namespace in the cluster.   
   
When you create a cluster by default K8s gives you 4 namespaces out of the box.   
   
To list namepsaces - `kubectl get namepsace`   
   
The Kubernetes-dashboard namespace is shipped automatically in [kubernetes.minikube](../devlog/kubernetes.Minikube.md)(it is specific to minikube installation).   
   
1. `kube-system`   
   
It is not meant for your use, you shouldn't modify it. The components that are deployed on `kube-system` are system processes. They're from master and managing processes or kubectl.   
   
2. `kube-public`   
   
It has publicly accessible data. A [kubernetes.ConfigMap and Secret](../devlog/kubernetes.ConfigMap%20and%20Secret.md) which contains cluster information(accessible even without authentication).   
   
Run `kubectl cluster-info` to get this information.   
   
3. `kube-node-lease`   
   
It holds information about the heartbeats of nodes. Each node has associated lease object in namespace which contains information about that node's availability.   
   
4 `default`   
   
This is the namespace that is referenced by default for every Kubernetes command, and where every Kubernetes resource is located by default. Until new namespaces are created, the entire cluster resides in ‘default’.   
   
### Create your own namespace   
   
Run `kubectl create namespace <name-of-namespace>`   
   
OR   
   
Use namespace configuration file to create a namespace(recommended because you can integrate version control).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656236351/wiki/vahcacuyv9fjezvza8e4.png)   
   
### When to use namespace   
   
Resources can be grouped using namespaces. A way of logically grouping your resources inside the cluster.   
   
For example:   
   
   
- A namespace for your DBses and required resources.   
- A namespace for monitoring, where you can deploy [Prometheus](../devlog/prometheus.md) and all the stuff it needs.   
- A namespace for [elastic stack](../devlog/Elastic%20Stack.md), where the [ElasticSearch](../devlog/Elasticsearch.md), [kibana](../devlog/kibana.md) resources go.   
- A namespace for ngnix-ingress resources.   
   
They should be avoided if the project is not that large or doesn’t have that many users(as per official guide) but you can do it anyway instead of throwing everything in the default namespace and it may result in difficulty managing it as you’d have no overview of all your different resources.   
   
**Conflicts**   
   
Namespaces are also useful if you’ve multiple teams.   
To avoid conflicts such as deploying of the same application in a single namespace and having it overwritten by the other teams. You can use namespaces for different projects inside your cluster.   
   
**Resource sharing**   
   
Lets say you’ve one cluster and you want to host both staging and development environment in the same cluster(to utilize common resources without having to redeploy them for different environments).   
   
**Blue/Green deployment**   
   
You can have two different versions of production application that share common resources.   
   
**Limit Access and Resources**   
   
You can limit access and resources to namespaces when working with multiple teams. Minimizing the risk of one team accidentally interfering with the other. Each team will have their own secure, isolated environment.   
   
You can limit the resources each namespace consumes. You can allot each team a share of resources for their applications.   
   
### Characteristics of Namespace   
   
You can’t access most resources from another namespace.   
   
**Each NS must define it’s own ConfigMap**. Eg: You’ll need to create a ConfigMap for your namespace that is referencing a DB, you cannot use other namespace’s ConfigMap. The same applies for secrets(credentials of a shared service).   
   
What you can access from another NS is a **service**.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656237672/wiki/ijk9q4etvplakbc2gfc0.png)   
   
Where yellow is namespace and white is the service being referred in a ConfigMap.   
   
**Components that cannot be namespaced**   
   
These components live globally in a cluster, you cannot isolate them in a NS.   
Eg: Persistent Volumes, Nodes.   
   
List resources that are not bound to namespace   
   
`kubectl api-resources --namespaced=false`   
   
List resources that are bound to namespace   
   
`kubectl api-resources --namespaced=true`   
   
### Create resource in a namespace   
   
Run `kubectl apply -f mysql-configmap.yaml --namespace=my-namespace`   
   
OR include the destination namespace in the ConfigMap itself   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656238019/wiki/jwpagppds4pc1qjvsa2p.png)   
   
### Get component created in a specific NS   
   
`kubectl get configmap -n my-namespace`   
   
Because by default **it’ll only the default namespace** if you don’t specify.   
   
### Change active NS   
   
Switch the default NS to your choice of NS   
   
`kubectl` doesn’t have an solution for this but `kubens` does!   
   
Install `kubectx` which will install `kubens` as well.   
   
`kubens` ran without options will return all the NSes and highlights active NS.   
   
`kubens my-namespace` will switch the active NS to `my-namespace`