---
created: 1661600945856
desc: Connecting to Applications inside cluster
id: ivx7g5iog7lcs18v7h0dicw
title: Services
updated: 1661605539658
---
   
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