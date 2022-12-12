---
created: 1653409437988
desc: ''
id: gbeh61d6hvbmxxy63chp81b
title: Kubernetes
updated: 1664526172325
---
   
Kubernetes is an open-source system for automating deployment, scaling, and management of [containers & images](/not_created.md) in different environments; [cloud](../devlog/cloud.md), [VM](../devlog/vm.md)s or physical environments. It is a container orchestration tool. Developed by Google.   
   
To understand what Kubernetes is good for, let's look at some examples:   
   
   
- You would like to run a certain application in a container on multiple locations. Sure, if it's 2-3 servers/locations, you can do it by yourself but it can be challenging to scale it up to additional locations.   
- It can get challenging to perform updates and changes across hundreds of containers.   
- Handle cases where the current load requires to scale up (or down).   
- If you are big team of engineers (e.g. 200) deploying applications using containers and you need to manage scaling, rolling out updates, etc. You probably want to use Kubernetes.   
- The rise of [microservices](../devlog/microservices.md) caused increased usage of container technologies.   
- Application nowadays comprise of multiple; hundreds to thousands of containers. Managing them using custom scripts can be a pain.   
- Container orchestration offers:   
  - High availability or no downtime.   
  - Scalability or high performance.   
  - Disaster recovery - backup, restore, etc.   
   
## What Kubernetes objects/components are there?   
   
   
- Pod(s)   
- Service   
- ReplicationController   
- ReplicaSet   
- DaemonSet   
- Namespace   
- ConfigMap   
   
> Tip: You can use [kubernetes.kubectl](../devlog/kubernetes.kubectl.md) to deploy applications, inspect and manage cluster resources, and view logs.   
   
### Pods   
   
> A pod is a collection of containers sharing a network, acting as the basic unit of deployment. All containers in a pod are scheduled on the same node.   
   
An abstraction over a container - a pod creates a layer on top of a container. Usually, only one application is running per pod. You don't directly create pods. You create deployments.   
   
Kubernetes offers a virtual network out of the box. Each pod gets its own IP Address. Which they can use to communicate with each other. It is an internal [IP Address](../devlog/ip%20address.md).   
   
They're ephemeral, meaning they are not persistent, they can die if the application crashes or if you run out of resources. A new one will be created automatically with new IP Address. To help with this, [kubernetes.sevices](/not_created.md) is used.   
   
### Service and Ingress   
   
   
- Static IP Address that can be attached to each pod. Life cycle of a service and a pod are not connected. Even if the pod dies, the service will still be there.   
- To make the application accessible through a browser, an external service needs to be created that opens communication from external sources. For a database, you'd have an internal service.   
- It also acts as a load balancer. It will catch a request and forward it to the node that is least busy.   
- **Ingress** is another component of Kubernetes that forwards request to the service. It makes URL more suitable for the end user.   
   
### ConfigMap and Secret   
   
   
- **ConfigMap** acts as an external configuration file. It is a way to store configuration data that is not in the code. Like a database URL that a pod utilizes.   
- To store username and password, **Secret** is used. It is not stored in plain text, it is base64 encoded (this does not mean encryption).   
   
### Volumes   
   
   
- Volumes are used to persistently store data(logs, databases, etc.).   
- It basically attaches a physical storage - a hard drive or a network drive(local or remote) - to a pod.   
- K8s explicitly doesn't manage persistent data.   
   
### Deployment and StatefulSet   
   
   
- To reduce down time - to make it fault tolerance - you can replicate everything(a node). That is connected to the same service.   
- This replication of the pod isn't done manually. Instead you'd define a blueprint(template) and tell it how many replicas you want it to run. This is called **Deployment**.   
- It is a abstraction over pods.   
- Deployment is used to create StateLess applications.   
- In practice, you'd be working with deployments not with pods.   
- You cannot replicate databases with Deployment, since databases have states and it can be prone to inconsistencies if deployments are used to replicate them.   
- **StatefulSet** are used to replicate databases or to create stateful applications. It also take care of scaling them up or down. It makes sure database reads and writes are synchronized.   
- Deploying StatefulSet applications can be tedious on K8s. It is a common practice to host database applications outside K8s and only have StateLess applications inside K8s cluster.   
   
## Kubernetes Architecture   
   
### Worker Machines/Nodes   
   
> A Node is a worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the control plane. A Node can have multiple pods, and the Kubernetes control plane automatically handles scheduling the pods across the Nodes in the cluster.   
   
   
- Each node has multiple pods running on it.   
- There are 3 process that must be installed on each node that are used to schedule and manage the pods.   
- Nodes are the cluster service that actually do that work.   
   
The three processes are:   
   
1. Container runtime   
   
   - [Docker](../devlog/docker.md)   
   - [cri-o](/not_created.md)   
   - [conatinerd](/not_created.md) (Most popular)   
2. Kubelet - is the process that actually schedules the pods and the containers underneath. It is the process of Kubernetes that has interfaces with both container runtime and the node(machine) itself. It assigns the resources etc.   
3. Kube Proxy - is the process that forwards the traffic from services to the pods. It has intelligent forwarding logic inside that makes sure the communication works in a performant way with low network overhead.   
   
### Master Node/Control Plane   
   
All the managing processes are taken care by the Master node inside the K8s cluster. There are 4 processes that are installed on the master node; these are completely different processes from Worker Nodes that control the cluster state and the Worker Nodes.   
   
1. `kube-apiserver` - if you want to deploy a new application on a K8s cluster, you will interact with this using a client such as Kubernetes dashboard, a CLI tool like Kubelet. It is like a cluster gateway. It receives the initial request(changes) needed to made on the cluster or queries from the cluster and also takes care of authorization.   
2. `kube-scheduler` - intelligently decides which Worker Node the next component will run on. It estimates the resources required for your request and decides where a new pod is to be scheduled.   
3. `kube-controller-manager` - when pods die on a node, it detects state changes and tries to recover the cluster state. It makes the request to the scheduler to restore those dead pods. Scheduler does its thing.   
4. `etcd` - Key value store that stores the cluster state. It is the brain of the cluster. Every change inside the cluster is saved in this key value store. etcd is where the scheduler gets its info from. The actual application's data is NOT stored on etcd.   
5. `cloud-controller-manager` - This component can embed cloud-specific control logic - for example, it can access the cloud provider’s load balancer service. It enables you to connect a Kubernetes cluster with the API of a cloud provider. Additionally, it helps decouple the Kuberneters cluster from components that interact with a cloud platform, so that elements inside the cluster do not need to be aware of the implementation specifics of each cloud provider.   
   
   - This cloud-controller-manager runs only controllers specific to the cloud provider. It is not required for on-premises Kubernetes environments.   
   
A K8s cluster is made up of multiple master nodes. Each master node runs its own processes. API Server is load balanced and etcd store does a distributed storage across all master nodes. They don't take a lot of resources compared to the worker nodes as their job is just delegating work.   
   
**Change in Terminology** from Master Node to Control Plane:   
   
   
- The label applied to control-plane nodes "node-role.kubernetes.io/master" is now deprecated and will be removed in a future release after a GA deprecation period.   
- Introduce a new label "node-role.kubernetes.io/control-plane" that will be applied in parallel to "node-role.kubernetes.io/master" until the removal of the "node-role.kubernetes.io/master" label.   
   
> — via [kubernetes/CHANGELOG-1.20.md at master · kubernetes/kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.20.md#urgent-upgrade-notes)   
   
   
---   
   

   
Minikube is a tool that lets you run Kubernetes locally. Minikube runs a single-node Kubernetes cluster on your personal computer so that you can try out Kubernetes, or for daily development work.   
   
It is a one node cluster, master and worker process run on one node. It comes with [Docker](../devlog/docker.md) preinstalled. It runs via VM or a hypervisor.   
   
## Resources   
   
   
- [minikube start | minikube](https://minikube.sigs.k8s.io/docs/start/)
   
   

   
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
   
   

   
### Kubernetes deployment configuration file   
   
If a deployment does not exist, it will be created. If it exists, it will be updated.   
   
`kubectl apply -f deployment.yaml`   
`kubectl apply -f config-file-nginx.yaml`   
   
It is used for creating and configuring K8s clusters. There are 3 parts to it:   
   
1. Metadata   
2. Specification   
   
   - Attributes are specific to the `kind`   
3. Status (auto-generated and added by kubernetes)   
   
   - Kubernetes will compare the desired with the actual state and if the desired state ≠ actual state, K8 will try to fix it.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655117494/wiki/ipq3mbgswsrb0ufg7hrt.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655117667/wiki/fakkxkxbdvspydlfnd4f.png)   
   
   
- The status is constantly updated, it gets it’s data from `etcd`.   
- The format of the configuration file is [languages.YAML](../devlog/languages.YAML.md) format.   
- The code is stored along with the source code of your application or it can have it's own repository.   
- The configuration file is structured as a "template" or a "blueprint" .   
- The connection is made using "selectors" and "labels".   
- Pods gets the label through the template blueprint.   
- This label is matched by the selector.   
- To get the configuration of a running deployment, use `kubectl get deployment deployment-name -o yaml`   
  - You'll find that a lot of information will be auto-generated by Kubernetes.   
- To copy a deployment you already have, you'll have to remove auto-generated stuff and clean the configuration file before creating a deployment from it.   
- You can use the configuration file to delete a deployment. `kubectl delete -f deployment.yaml`   
   
### Creating a Secret   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655127535/wiki/ag8cc3fib3l5qtkvwasf.png)   
   
When you store values, don’t use plain text, encode them in base64. For example: `echo -n "somevalue" | base64`   
   
`kubectl apply -f secrets.yaml`   
   
Secret once created can be referenced in your deployment configuration files.   
   
Example of secret being referenced:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655127895/wiki/lmddjxbristzwqipuuy3.png)   
   
### Creating a Service   
   
Deployment and Service can be put in a single file. You don’t define a type unlike an External Service where type is defined because Internal Service or ClusterIP(it gives an internal IP Address) is the default.   
   
Example of a Service configuration   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655128136/wiki/vepvw9yubv8izozijvjo.png)   
   
Reapply the `deployment.yaml` and the newly added Service will also be created.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655128207/wiki/ljbcr1cfavkzz0lsbjd1.png)   
   
To validate if the Service is attached to the correct Pod, you can run `kubectl describe service service-name` and cross check `endpoints` IP Address with the Pod’s `kubectl get pod -o wide`.   
   
### Creating ConfigMap   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655128682/wiki/mow4k1vejxaungybxje8.png)   
   
ConfigMap must already be created in the K8s cluster before referencing it.   
   
`kubectl apply -f configmap.yaml`   
   
Referencing ConfigMap   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655128847/wiki/odygjn3izkrd8gotfhlq.png)   
   
### Creating an External Service   
   
It is very similar to a typical Service. Internal service also acts like a load balancer but an External Service acts like loan balancer by accepting external request by assigning the service an external [IP Address](../devlog/ip%20address.md).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655129162/wiki/gpts0wcs1wrdij7txbfc.png)
   
   

   
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
   
   

   
**Overview**   
   
   
- What is a Kubernetes service and when do we need it?   
- Different Service types:   
  - ClusterIP   
  - NodePort   
  - Headless   
  - LoadBalancer   
- What is the different between these services and which service to use?   
   
   
---   
   
In Kubernetes, each pod has its own (internal) IP address. But pods are ephemeral and when a pod dies and a new one is created in it's place, it gets assigned a new IP address. Hence, it doesn't make sense to use a pod's IP address directly.   
   
A service basically offers a static IP address that persists even when a pod dies. It also provides loadbalancing when you've replica pods to direct traffic automatically to pods. It gives a layer of loose coupling within the cluster and also outside the cluster.   
   
## ClusterIP Services   
   
Default type of a service, when you create a service with type undefined, it'll automatically take ClusterIP as a type.   
   
Lets say you've a microservice app deployed in a cluster. You've a pod with a microservice container running inside that pod. You also have a side-car container that collects the logs of the microservice and sends it to some destination DB. Microservices container running on port 3000. Logging container running on port 9000. This means that the two ports are now open and accessible inside the pod. The pod will get an IP address from a range assigned to that Node.   
   
**Internal Service** or **Service**   
   
Is a component in Kubernetes just like a pod but it's not a process. It is an abstraction layer that basically represents an IP address. Service also gets an IP address and a port at which it's accessible. Ingress will handover the request to the Service(using it's IP address and port).   
   
## Service Communication: selector   
   
> How does service forward the request to pod and at which port.   
   
Enter "selector"   
   
A service identifies it's member pod's or it's endpoint pods using "selector" attribute. In the service configuration file we specify the selector attribute that has a key-value pair defined as a list. This key-value pairs are labels that pods should have to match a selector.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661965565/wiki/yhzpnx3s3fufhmew9a9e.png)   
   
Labels are arbitrary names.   
   
## Service Communication: port   
   
> If a pod has multiple ports open where two different applications/containers are listening inside the pod…how does service know which port to forward the request to?   
   
In the service configuration file, you can define the target port under “ports”.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661965767/wiki/njjjiyqax12vfipzq6jg.png)   
   
**Service port is arbitrary whereas `targetPort` must match the port, the is container listening at.**   
   
## Service Endpoints   
   
When you create a service, Kubernetes creates an endpoint object that has the same name as service itself which it uses to keep track of which pods are the members/endpoints of the service.   
   
## Multi-port Services   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661967459/wiki/ege96sfbgdgsua6dtxog.png)   
   
If it’s only one port you don’t need to define a name but when you’ve multi ports defined in a service, you’ve to name those ports.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661967510/wiki/ffxgzt4f546br98prewo.png)   
   
## Headless Service   
   
What if a client wants to communicate one of the pod’s directly(without a service between them) and selectively. Or if the endpoint pods want to communicate with each other directly without going through the service.   
   
In such a case, you can use Headless Service.   
   
Use case: Stateful applications, like databases. In these cases pod replicas are not identical, rather, each one has it’s individual state and characteristics.   
   
What if only master is allowed to write to DB and the other worker nodes need to connect with master and sync the changes and new worker nodes will need to connect with the worker node with latest changes and sync the changes.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661967789/wiki/ukt98cgbmejatrqrv7bn.png)   
   
**Headless Service**   
   
For clients to connect to all pods individually, it needs to figure out the IP address of each pod. You can achieve this with either:   
   
   
- API call to K8s API server - which will return a list of pods and their IPs.   
  - Inefficient   
  - Relies too much on K8s API   
- DNS Lookup   
   
   
  - Kubernetes allows clients to discover pods IP addresses through DNS lookups.   
  - When a client performs DNS lookup for a service, the DNS server returns a single IP address that belongs to a service(the default method).   
  - Set `clusterIP: None` to return pod IP address instead.   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1661968153/wiki/s9ucfffhn1xuzhjoc2fg.png)   
   
   
  - When you create a service this way, no ClusterIP will be assigned which you can check with `kubectl get svc`.   
   
## NodePort Service   
   
When we define a service configuration, we can specify a type of the service.   
   
The type attribute can have one of these 3 values:   
   
   
- ClusterIP (default)   
- NodePort   
- LoadBalancer   
   
NodePort basically creates a service that is accessible on a static port on each worker node in the cluster. Whereas ClusterIP only accessible within cluster(no external traffic can directly address).   
   
External traffic(browser requests ) has access to fixed/static port on each Worker Node at IP address of Worker Node and the NodePort. The port of the service: when we create a NodePort service a ClusterIP service to which NodePort service will route is automatically created.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661969515/wiki/o9h50bbcr4yzs4z9pd1l.png)   
   
NodePort services are not secure because external clients have access to worker nodes directly. In the production, you probably would never use NodePort for external connection, you’d use Ingress or LoadBalancer.   
   
## LoadBalancer Service   
   
A service becomes accessible externally through a cloud provider’s LoadBalancer functionality.   
   
When we create a LoadBalancer service, NodePort and ClusterIP services are created automatically by K8s to which the external LoadBalancer of the cloud provider will route the traffic to.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661969712/wiki/spne3ruynuson09gxs9e.png)   
   
   
- Essentially, LoadBalancer service is an extension of NodePort service which itself is an extension of ClusterIP.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661969796/wiki/unynv7pruo4tadoagwju.png)
   
   

   
## [kubernetes.services](/not_created.md) vs Ingress   
   
External service would require you to open IP address and port when making/accepting a requests from a web browser. But ingress you wouldn't have to do that.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661978549/wiki/nfmupnio0d59d89tkouu.png)   
   
**External service**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661978644/wiki/v4dwviww89miqlwamr4k.png)   
   
**Ingress**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661978666/wiki/ncde01hcej9udet4pnt3.png)   
   
**Ingress vs Internal service**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661978786/wiki/wh1xxr8j8zbwyhj0mgct.png)   
   
   
---   
   
Host should be a valid domain address and you should map domain name to Node’s IP address, which is the entrypoint.   
   
## Configure Ingress   
   
The YAML created Ingress component alone isn’t enough. You need an implementation for those routing rules to work. You accomplish this using **Ingress Controller**   
   
1. **Ingress Controller** - a pod, a set of pods that run on a node in your K8s cluster and does evaluation and processes Ingress rules. It manages all the redirections and is the entrypoint to cluster for all the requests to domains or subdomains that you’ve configured.   
   
   You’ve to choose from the many third-party implementations of Ingress Controller. [Ingress Controllers | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)   
   
   The one from K8s is - K8s Ngnix Ingress Controller.   
   
2. Configure the environment on which your cluster is running.   
   
   One of the ways is:   
   
   ![](https://res.cloudinary.com/zubayr/image/upload/v1661979391/wiki/mv9v4o2snefydunqfszj.png)   
   
   If your cluster is running on bare metal, you’ll need to configure some kind of entrypoint yourself. Either inside the cluster or outside as separate server   
   
Essentially:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661979503/wiki/uvzwz90ug05w2tigltas.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661979645/wiki/ksnzhmzwm60dxrgfcqrt.png)   
   
No server in K8s cluster will be accessible from outside because of this proxy server which’ll redirect the traffic to ingress controller and ingress controller which rule applies to that request and how to proceed.   
   
## Configure Ingress on [kubernetes.Minikube](../devlog/kubernetes.Minikube.md)   
   
1. `minikube addons enable ingress` to install Minikube Ingress controller.   
   
   - Automatically starts the K8s Ngnix implementation of Ingress controller.   
   - To verify `kubectl get pod -n kube-system`   
2. Create Ingress rule   
   
   - Let’s add rules for K8s dashboard to access it from a browser using a domain name.   
   
```yaml
# dashboard-ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
	name: dashboard-ingress
	namespace: kubernetes-dashboard # same as service and pod
spec:
  rules:
  - hosts: dashboard.com # resolve ip address to host name
    http:
      paths:
      - backend:
        serviceName: kubernetes-dashboard
        servicePort: 80
```
   
   
`kubectl apply -f dashboard-ingress.yaml`   
`kubectl get ingress -n kubernetes-dashboard`   
   
Locally, you can map the host dashboard.com to the IP address of the ingress by editing `/etc/hosts`   
   
## Configure Default Backend in Ingress   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661985173/wiki/q996ghiy8je1viuerukh.png)   
   
For custom error messages   
   
## More use cases   
   
**Multiple paths for same host**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661985269/wiki/rc5ojzsdgff1d34emk8j.png)   
   
**Multiple sub-domains or domains**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661985377/wiki/gqucmk4ci95y0ovgz1wr.png)   
   
## Configuring TLS Certificate   
   
So far, we’ve only seen Ingress configuration for `http` requests but we can configure `https` forwarding in Ingress.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661985495/wiki/glffyk5psabb8ktlr8dx.png)   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661985506/wiki/kw10sonbzjrlwobk68x5.png)   
   
   
- Data keys need to be named "`tls.crt`" and “`tls.key`“.   
- Values are file contents NOT file paths/locations.   
- Secret component must be in the same namespace as the Ingress component.
   
   

   
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
   
   

   
**When to use ConfigMap and Secret Volumes**   
   
Think of applications that take configuration files as parameters when they start. Like [prometheus](../devlog/prometheus.md), [Elasticsearch](../devlog/Elasticsearch.md), [Ngnix](/not_created.md) or your own application file that requires a properties file. Or if your app require external services that it communicates with that are secured using password, you’d need a credentials file or a certificates files.   
   
ConfigMap and Secret are used for external configuration of individual values or files that Pod/container can read.   
   
## ConfigMap and Secret for mounting files   
   
Create files that can be mounted onto the Pod and the container there after.   
   
```yaml
#config-file.yaml
---
apiVersion: va
kind: ConfigMap
metadata:
	name: mosquitto-config-file
data:
	mosquitto.conf: | # name of the file
		log_dest stdout # contents of the file
		log_type all
		log_timestamp true
		listener 9001
```
   
   
```yaml
# secret-file.yaml
---
apiVersion: v1
kind: Secret 
metadata:
	name: mosquitto-secret-file 
type: Opaque
data: 
	secret.file: | 
		contents of the file - base64 encoded
```
   
   
```yaml
# secret-certificate.yaml
apiVersion: v1
kind: Secret 
metadata: 
	name: my-secret
	type: Opaque
data:
	cacert.pem: |
		base-64-encoded value of PEM certificate
```
   
   
## Mosquitto Demo   
   
   
- Overwrite `mosquitto.conf`.   
- Adding passwords file.   
   
A ConfigMap and a Secret file for mosquitto Pod.   
   
**Mosquitto Pod without any Volumes**   
   
No files mounted, starts without any persistence.   
   
```yaml
# mosquitto-without-volumes.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
	name: mosquitto
	labels:
		app: mosquitto
	spec:
		replicas: 1
		selector:
			matchLabels:
				app: mosquitto
		template:
			metadata:
				labels:
					app: mosquitto 
			spec:
				containers:
					- name: mosquitto 
						image: eclipse-mosquitto:1.6.2
						ports:
							- containerPort: 1883
```
   
   
`kubectl -f mosquitto-without-volumes.yaml`   
`kubectl get pod`   
`kubectl exec -it <pod-name> -- /bin/sh`   
   
**Overwrite mosquitto conf**   
   
Make sure Secret and ConfigMap have been created.   
   
A new mosquitto deployment that uses ConfigMap and Secret volumes(overwrite).   
   
```yaml
# mosquitto-with-volumes.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
	name: mosquitto
	labels:
		app: mosquitto
	spec:
		replicas: 1
		selector:
			matchLabels:
				app: mosquitto
		template:
			metadata:
				labels:
					app: mosquitto 
			spec:
				containers:
					- name: mosquitto 
						image: eclipse-mosquitto:1.6.2
						ports:
							- containerPort: 1883
						volumeMounts:
							- name: mosquitto-config 
								mountPath: /mosquitto/config # path in the FS inside the container to overwrite
							- name: mosquitto-secret 
								mountPath: /mosquitto/secret
								readOnly: true
				volumes: 
					- name: mosquitto-config
						configMap:
							name: mosquitto-config-file 
					- name: mosquitto-secret
						secret: 
							secretName: mosquitto-secret-file
```
   
   
   
- Volumes mounted into the Pod.   
- Mount volumes into container.   
   
`kubectl -f apply -f mosquitto-with-volumes.yaml`   
`kubectl get pod`   
`kubectl exec -it <pod-name> -- /bin/sh`   
   
Secret dir and secret file will be created.
   
   

   
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
   
   

   
**Overview**   
   
   
- What is Helm?   
- What are Helm Charts?   
- How to use them?   
- When to use them?   
- What is Tiller?   
   
## What is Helm   
   
1. Package Manager   
   
It is like `apt`, `yum` or `brew` for Kubernetes. A convenient way of packaging Kubernetes YAMl files and distributing them in public and private repository.   
   
A bundle of YAML files that can be used to replicate a Deployment anywhere is called a **Helm Chart**. They can be stored on Helm repository and download existing Helm Charts people have created.   
   
Commonly used Deployments like DB applications, Elasticsearch, MongoDB or monitoring applications like Prometheus that require a complex setup all have charts available in some Helm repository.   
   
You can simply reuse a configuration without additional effort using Helm.   
   
There are public and private repositories to share within the organization.   
   
2. Templating Engine   
   
Helm can also be used as a templating engine.   
   
Let's say you've a bunch of microservices applications that require same configuration except for some attributes/values that will be different. Instead of writing separate YAMl config files for different microservices. You can use Helm to define a common blueprint for all of the microservices. Dynamic values are replaced by placeholders.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662077090/wiki/v3ahdokiky8lvjodawde.png)   
   
You can take values from external configuration like `values.yaml` where you can define the values to be used or u can use `--set` flag to define values.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662077155/wiki/m9penrvbkodbcinib7k4.png)   
   
Another use case: **Same applications across different environments**   
   
Instead of deploying, individual YAML files on each cluster, you can package them up into your own Chart that will have all the necessary YAML files that Deployment needs and you can deploy it in different environments using one command making deployment process easier.   
   
## Helm Chart Structure   
   
**Directory Structure**:   
   
```bash
myChart/  # name of the chart
	Chart.yaml # meta info about the chart
	values.yaml # values for the template files, default values that you can overwrite
	charts/ # chart dependencies
	templates/ # the actual template files
	...
	# optionally, you can have Readme, License files
```
   
   
`helm install <chartname>`   
   
## Values Injection   
   
The default values (defined in `values.yaml`) can be overwritten in a few ways.   
   
1. Use `--values` flag to provide alternative values file.   
   
`helm install --values=my-values.yaml <chartname>`   
   
The resultant `.Values` object would’ve merged the values from `values.yaml` and `my-values.yaml` overwriting values selectively as per defined values.   
   
2. Use `--set` flag to define values directly on the command line.   
   
`helm install --set version=2.0.0`   
   
## Release Management   
   
In version Helm v2, the Helm installation comes in 2 parts:   
   
   
- `helm cli` (Client)   
- `tiller` (Server)   
   
The client forwards requests to server, that does the actual work on the target cluster.   
   
Release management is offered on this version of Helm.   
   
Whenever you create or change deployment, `tiller` will store a copy of the configuration for future reference thus creating a history of chart execution.   
   
So, in future when you do `helm upgrade <chartname>`, changes are applied to existing deployment instead of creating a new one.   
   
If an update goes wrong, you can rollback to previous state using `helm rollback <chartname>`.   
   
**Downsides of Tiller**   
   
It has too much power inside Kubernetes cluster. It can CRUD components and it has too many permissions. It can be a big security issue.   
   
In the newer Helm v3, they removed the Tiller and it’s a simple Helm binary with Helm v3.   
   
## Labs   
   

   
**Overview**   
   
Deploying a managed K8s Cluster using [LKE](../devlog/LKE.md). We'll deploy a replicated DB and configure it's persistence and make it accessible through a UI client from browser using Ingress. We'll achieve all of this using [kubernetes.helm](../devlog/kubernetes.helm.md).   
   
   
- Deploy [mongodb](../devlog/mongoDB.md) using Helm.   
- 3 replicas(replicated MongoDB) using [kubernetes.StatefulSet](../devlog/kubernetes.StatefulSet.md).   
- Configure data persistence with Linode's cloud storage.   
- Deploy UI client `mongo-express` for MongoDB to access it from browser.   
  - Through which we'll configure Ngnix Ingress.   
  - We'll deploy Ingress controller in the cluster and configure Ingress rule in order to demonstrate handling browser requests in the cluster.   
   
   
The concepts demonstrated in this process can be used across different cloud providers.   
   
## Create cluster on LKE   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662082498/wiki/pahsvlhwumz8lfqqjhwt.png)   
   
Since managed K8s cluster takes care of Master Nodes, you’ll only need to create Worker Nodes.   
   
To access the cluster from your local machine and run command using `kubectl` download the `<cluster>-kubeconfig.yaml` file from the LKE dashboard.   
   
Set `kubeconfig.yaml` as an environmental variable.   
   
`export KUBECONFIG=<cluster>-kubeconfig.yaml`   
   
`kubectl get node` to verify connection.   
   
## Deploy MongoDB StatefulSet   
   
You can achieve this in two ways:   
   
1. Create all configuration files yourself.   
   
	- StatefulSet config file   
	- Services   
	- Other configurations   
2. Use bundle of those config files (Helm Chart).   
   
We’ll do with Helm Chart way.   
   
Let’s use the Helm Chart provided by [bitnami/charts](https://github.com/bitnami/charts/tree/master/bitnami/mongodb).   
   
Make sure to install Helm - [Installing Helm](https://helm.sh/docs/intro/install/).   
   
When you execute Helm commands, it’ll execute it against the cluster you’re connected to.   
   
`helm repo add bitnami https://charts.bitnami.com/bitnami`   
   
`helm search repo bitnami/mongodb`   
   
   
To check what default values you can overwrite, check the description(Readme) for the chart > Parameters.   
   
   
- For `architecture` parameter, choose `replicaset` for multiple replicas.    
- We want Helm Chart to use the StorageClass of Lindode’s Cloud Storage.   
   
Create `values.yaml` to overwrite the default paramters.   
   
```yaml
# values-mongodb.yaml
architecture: replicaset 
replicaCount: 3
persistence:
	storageClass: "linode-block-storage"
auth:
	rootPassword: secret-root-pwd
```
   
   
`helm install mongodb --values path/to/values-mongodb.yaml bitnami/mongodb`   
   
>  Syntax: `helm install [our name] --values [values file name] [chart name]`   
   
`kubectl get all` to check all the components that got created.   
   
`kubectl get secret` to find the root password that was provided in the values file.   
   
For `linode-block-storage` StorageClass; When the StatefulSet was created for each Pod a physical storage was created. For each physical storage a PV was created and mounted to the Node where the Pod lives.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662085841/wiki/cng9dynsyeksij6tynlm.png)   
   
## Deploy `mongo-express`   
   
`mongo-express` is going to be only 1 Pod. We’ll create our own configuration file instead of using Helm Chart.   
   
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-express
  labels:
    app: mongo-express
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo-express
  template:
    metadata:
      labels:
        app: mongo-express
    spec:
      containers:
      - name: mongo-express
        image: mongo-express
        ports: 
        - containerPort: 8081
        env:
        - name: ME_CONFIG_MONGODB_ADMINUSERNAME
          value: root
        - name: ME_CONFIG_MONGODB_SERVER
          value: mongodb-0.mongodb-headless
        - name: ME_CONFIG_MONGODB_ADMINPASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb
              key: mongodb-root-password
---
apiVersion: v1
kind: Service
metadata:
  name: mongo-express-service
spec:
  selector:
    app: mongo-express
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
```
   
   
`kubectl apply -f mongo-express.yaml`   
   
`kubectl get pod`   
   
`kubectl get logs <pod-name>`   
   
With this we’ll have MongoDB running in our cluster, data is being persisted.   
   
`mongo-express` is an internal service, we still have to open it to the browser for external requests.   
   
## Configure Ingress   
   
1. Deploy Ingress Controller   
2. Create Ingress rules   
   
   
**Deploy Ingress Controller**   
   
Use Helm Chart for Ingress Controller. We’ll use `ngnix-ingress` controller.   
   
```fallback
helm repo add nginx-stable https://helm.nginx.com/stable
```
   
   
```fallback
helm repo update
```
   
   
```fallback
helm install ngnix-ingress nginx-stable/nginx-ingress --set controller.publishService.enabled=true
```
   
   
   
— Via [Installation with Helm | NGINX Ingress Controller](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-helm/)   
   
`kubectl get pod` to check if `ngnix-ingress` package was installed.   
   
**Define Ingress Rules**    
   
As you create the Ingress controller, a NodeBalancer (cloud native) will also be created, which will become the entrypoint into the cluster.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662088338/wiki/nqvcokukqo2owdt0eadn.png)   
   
`kubectl get svc` to check if ingress service was created.   
   
The LoadBalancer service type of the Ingress will also have an external IP which will be basically the same as the NodeBalancer’s.   
   
```yaml
# ingress.yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: nginx
  name: mongo-express
spec:
  rules:
    - host: host-name.nodebalancer.linode.com # in prod, it'll be my-app.com, domain must point to IP of NodeBalancer.
      http:
        paths:
          - path: /
            backend:
              serviceName: mongo-express-service
              servicePort: 8081
```
   
`kubectl apply -f ingress.yaml`   
   
`kubectl get ingress`   
   
Now, if you go to `<host-name>.nodebalancer.linode.com` you’ll find the `mongo-exress` UI.   
   
The data will persist even if you delete the Pods and if you create them again, the PV will be attached back automatically.   
   
   
**Delete Charts**   
   
`helm ls`   
   
`helm uninstall mongodb`

   
   

   
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
   
   

   
**Overview**   
   
   
- Authentication and Authorization in K8s   
- How to configure users, groups and their permissions.   
- Authorization with **R**ole **B**ased **C**ontrol (RBAC).   
- Which K8s resources to use define permissions in the cluster.   
   
## Why do you need Authorization?   
   
How do you manage permissions in a cluster? Admins need elevated access whereas Users have limited access.   
   
As a security best practice we should follow the Principle of least privilege.   
   
**RBAC** = Role Based Access Control   
   
## Role   
   
When you've multiple namespaces in your cluster where each developer team deploys applications in different namespace. How do you make sure that each team only has access to their namespace and the resources that belong to that namespace.   
   
   
- With Role component you can define namespaced permissions.   
- Role is bound to a specific namespace.   
- It defines what resources(Pod, Deployment, Service etc) you've access to in that namespace.   
- and what actions(list, get, update, delete etc) you can perform with/on those resources.   
   
For different developer teams, you can create a specific role and define permissions for it.   
   
Role doesn't define WHO gets these permissions. You need to attach Role definition to a person or team.   
   
## RoleBinding   
   
With RoleBinding you can basically link(bind) a Role to a User or a User Group.   
   
## CluserRole   
   
For Admins that usually do cluster-wide operations, Role cannot be used in this scenario as it is limited to a namespace and Admins need cluster-wide access. Enter ClusterRole.   
   
It defines what resources has what permissions - cluster-wide.   
   
## ClusterRoleBinding   
   
After creating a ClusterRole, you can bind the ClusterRole to a Group of Admins(Users) using ClusterRoleBinding.   
   
## Users and Groups   
   
**How do we create Users and Groups**   
   
   
- K8s doesn't manage Users natively.   
- Admins can choose different authentication strategies.   
- No K8s Objects exist for representing user accounts.   
- It relies on external sources for creating and managing Users, Groups.   
- This external source can be a static file with user details such as username and token.   
- It can also be certificates signed by K8s or by a 3rd party identity service like [LDAP](../devlog/ldap.md)   
   
A K8s Admin configures one of this external sources in the cluster and the API Server(Control Plane component) handles all the authentication requests coming in. It uses one of the configured authentication methods(sources).   
   
`kube-apiserver --token-auth-file=/users.csv [other-options]`   
   
```csv
# users.csv
05c2b1e0303d04a85521c8eb3a4a1019m, user_1, u1001
4e02489b29e13918506ffffe3cd5ce1e, user_2, u1002
c1b200529b999126865486bea54b77af, user_3, u1003
```
   
   
```csv
# users-group.csv
05c2b1e0303d04a85521c8eb3a4a1019m, user_1, u1001, group1
4e02489b29e13918506ffffe3cd5ce1e, user_2, u1002, group2
c1b200529b999126865486bea54b77af, user_3, u1003, group3
```
   
   
As for certificates, you'll have to manually create certs for different users or you(an Admin) can configure LDAP as authentication source for the API Server.   
   
## Service Accounts   
   
So far, we've seen how to configure permissions for Human Users. Let's see how we can configure permissions for Application Users.   
   
These applications can be inside the cluster or outside the cluster.   
   
An example for an internal application would be [prometheus](../devlog/prometheus.md). Microservices that might need access within their namespace. These applications could be communicating with other applications internally, or gathering information like a monitoring application.   
   
An example for external application could be a CI/CD Server deploying apps inside/to the cluster. An IaC tool like Terraform that configures the cluster itself.   
   
We want to make sure that applications only have permissions that they need to do their job properly.   
   
To define permissions for Application Users in K8s we've a K8s component that represents an Application User.   
   
**ServiceAccount**   
   
You create a ServiceAccount component for Application User with:   
   
`kubectl create serivceaccount sa1`   
   
You can then link(bind) this SA to a Role or ClusterRole with RoleBinding and ClusterRoleBinding respectively.   
   
## Example Config Files   
   
**Role**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
  - apiGroups: [""] # "" indicates the core API group
    resources: ["pods"]
    verbs: ["get", "watch", "list"]
```
   
   
**RoleBinding**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
# This role binding allows "jane" to read pods in the "default" namespace.
# You need to already have a Role named "pod-reader" in that namespace.
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
  # You can specify more than one "subject"
  - kind: User
    name: jane # "name" is case sensitive
    apiGroup: rbac.authorization.k8s.io
roleRef:
  # "roleRef" specifies the binding to a Role / ClusterRole
  kind: Role #this must be Role or ClusterRole
  name: pod-reader # this must match the name of the Role or ClusterRole you wish to bind to
  apiGroup: rbac.authorization.k8s.io
```
   
   
**ClusterRole**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: monitoring-endpoints
  labels:
    rbac.example.com/aggregate-to-monitoring: "true"
# When you create the "monitoring-endpoints" ClusterRole,
# the rules below will be added to the "monitoring" ClusterRole.
rules:
  - apiGroups: [""]
    resources: ["services", "endpoints", "pods"]
    verbs: ["get", "list", "watch"]
```
   
   
**CluserRoleBinding**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
# This cluster role binding allows anyone in the "manager" group to read secrets in any namespace.
kind: ClusterRoleBinding
metadata:
  name: read-secrets-global
subjects:
  - kind: Group
    name: manager # Name is case sensitive
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```
   
   
## Creating & Reviewing RBAC Resources   
   
You create these RBAC resources just like any other K8s component with `kubectl apply -f file.yaml` and view them using `kubectl get roles` or `kubectl describe role <role-name>`.   
   
## Checking API Access   
   
`kubectl` provides a `auth can-i` subcommand to quicky check if current user can perform a certain action.   
   
`kubectl auth can-i create deployments --namespace dev`   
   
Admins can also check permissions of other users.   
   
## Layers of Security   
   
We've two different levels of security in K8s.   
   
1. When receiving an incoming request, it'll check if the User has the permissions to even connect to the cluster.   
2. If authenticated, it'll check the user's authorization using RBAC after which it'll proceed with the User's request.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662243285/wiki/wb6baytfe6kb2ebz88rz.png)
   
   

   
Introduction to [microservices](../devlog/microservices.md) in [kubernetes](../devlog/kubernetes.md).   
   
**Overview**   
   
   
- Benefits of having Microservices.   
- Microservices in a K8s cluster.   
   
K8s emerged as a Platform for Microservices Applications.   
   
The traditional monolith applications that evolved into multiple smaller applications that can be developed, deployed and managed independently. Each business functionality is encapsulated into its own Microservice. This results in cleaner code, less interconnected logic, more fault tolerance.   
   
**How do Microservices communicate?**   
   
1. Service-to-Service API calls(interfaces).   
2. Third-party Message Broker application.   
   
   - Lesser code complexity.   
   - Redis   
   - RabbitMQ   
3. Service Mesh architecture.   
   
   - Instead of having a centralized message broker that handles all the communication, each MS has it's own helper program([SideCar Container](/not_created.md)) that handles the communication for that MS.   
   - Istio   
   
   
---   
   
**A DevOps engineer's responsibility in regards to MS**   
   
   
- You might get tasks like deploying an existing(already developed) MS application in a K8s cluster.   
- You need to have information about the MS to be able to deploy, you'll get this information from the Devs.   
  - How many total MS that you need to deploy?   
  - Which MS is talking to which MS?   
  - How are they communicating with each other?   
    - If they're using API calls, Message Broker or a Service Mesh.   
      - What application are they using to get this done?   
  - What DBs are they using or if there are any third-party services involved?   
  - On which Port does each MS run?   
- Using the information you can:   
  - Prepare the K8s env.   
  - Create Secret, ConfigMaps   
  - Deploy third-party services/apps.   
  - Create Deployment & Service manifest files for each MS.   
  - Decide which namespaces are the MS going to belong?
   
   
## etcd   
   
## Taints   
   
## DaemonSets   
   
## CRDs   
   
## Labs   
   
   
- [kubernetes.Deploying mongoDB and mongo-express in Kubernetes Cluster](../devlog/kubernetes.Deploying%20mongoDB%20and%20mongo-express%20in%20Kubernetes%20Cluster.md)   
- [kubernetes.Install a Stateful App using Helm](../devlog/kubernetes.Install%20a%20Stateful%20App%20using%20Helm.md)   
- [kubernetes.Deploying Images from private Docker repository](../devlog/kubernetes.Deploying%20Images%20from%20private%20Docker%20repository.md)   
- [kubernetes.Install Prometheus Stack in Kubernetes](/not_created.md)   
- [kubernetes.Deploy Microservices Application](../devlog/kubernetes.Deploy%20Microservices%20Application.md)   
- [kubernetes.helm chart for microservices](../devlog/kubernetes.helm%20chart%20for%20microservices.md)   
   
## Sidecar containers   
   
   
- [Container Design Patterns for Kubernetes - Part 1](https://www.weave.works/blog/container-design-patterns-for-kubernetes/)   
- [Kubernetes Sidecar Container | Best Practices and Examples](https://www.containiq.com/post/kubernetes-sidecar-container)   
   
## Resources   
   
   
- [Kube by Example Homepage](https://kubebyexample.com/)   
- [Concepts | Kubernetes](https://kubernetes.io/docs/concepts/_print/)   
- [An Ultimate Kubernetes Hands-on Labs and Tutorials | kubelabs](https://collabnix.github.io/kubelabs/)   
- [Kubernetes Architecture: 11 Core Components Explained | Spot](https://spot.io/resources/kubernetes-architecture-11-core-components-explained/)   
- [K8s Ecosystem Map – Navigate the K8s sea](https://k8smap.com/)   
- [Build Your First Kubernetes Cluster - Learn Kubernetes](https://learning.kasten.io/kubernetes/labs/first-kubernetes-cluster/)   
   
## Misc. Links   
   
   
- [Civo Kubernetes - Fast, Simple, Managed Kubernetes Service - Civo.com](https://www.civo.com/)   
   
## Look into   
   
   
- Kubernetes Diagram