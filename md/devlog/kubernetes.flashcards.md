---
created: 1664805011279
desc: ''
id: b8gvjjv1etr4f2tjjr1tymc
title: Flashcards
updated: 1664805493912
---
   
## What is Kubernetes? Why organizations are using it?   
   
Kubernetes is an open-source system that provides users with the ability to manage, scale and deploy containerized applications.   
   
To understand what Kubernetes is good for, let's look at some examples:   
   
   
- You would like to run a certain application in a container on multiple different locations and sync changes across all of them, no matter where they run   
- Performing updates and changes across hundreds of containers   
- Handle cases where the current load requires to scale up (or down)   
   
## When or why NOT to use Kubernetes?   
   
   
- If you manage low level infrastructure or baremetals, Kubernetes is probably not what you need or want   
- If you are a small team (like less than 20 engineers) running less than a dozen of containers, Kubernetes might be an overkill (even if you need scale, rolling out updates, etc.). You might still enjoy the benefits of using managed Kubernetes, but you definitely want to think about it carefully before making a decision on whether to adopt it.   
   
## What are some of Kubernetes features?   
   
   
- Self-Healing: Kubernetes uses health checks to monitor containers and run certain actions upon failure or other type of events, like restarting the container   
- Load Balancing: Kubernetes can split and/or balance requests to applications running in the cluster, based on the state of the Pods running the application   
- Operators: Kubernetes packaged applications that can use the API of the cluster to update its state and trigger actions based on events and application state changes   
- Automated Rollout: Gradual updates roll out to applications and support in roll back in case anything goes wrong   
- Scaling: Scaling horizontally (down and up) based on different state parameters and custom defined criteria   
- Secrets: you have a mechanism for storing user names, passwords and service endpoints in a private way, where not everyone using the cluster are able to view it   
   
<a name="kubernetes-hands-on-basics"></a>   
   
## What Kubernetes objects are there?   
   
   
- Pod   
- Service   
- ReplicationController   
- ReplicaSet   
- DaemonSet   
- Namespace   
- ConfigMap   
  ...   
   
## What fields are mandatory with any Kubernetes object?   
   
metadata, kind and apiVersion   
   
## What is kubectl?   
   
Kubectl is the Kubernetes command line tool that allows you to run commands against Kubernetes clusters. For example, you can use kubectl to deploy applications, inspect and manage cluster resources, and view logs.   
   
## What Kubernetes objects do you usually use when deploying applications in Kubernetes?   
   
   
- Deployment - creates the Pods () and watches them   
- Service: route traffic to Pods internally   
- Ingress: route traffic from outside the cluster   
   
## Why there is no such command in Kubernetes? <code>kubectl get containers</code>   
   
Becaused container is not a Kubernetes object. The smallest object unit in Kubernetes is a Pod. In a single Pod you can find one or more containers.   
   
## What actions or operations you consider as best practices when it comes to Kubernetes?   
   
   
- Always make sure Kubernetes YAML files are valid. Applying automated checks and pipelines is recommended.   
- Always specify requests and limits to prevent situation where containers are using the entire cluster memory which may lead to OOM issue   
   
## What is a Kubernetes Cluster?   
   
Red Hat Definition: "A Kubernetes cluster is a set of node machines for running containerized applications. If you’re running Kubernetes, you’re running a cluster.   
At a minimum, a cluster contains a worker node and a master node."   
   
Read more [here](https://www.redhat.com/en/topics/containers/what-is-a-kubernetes-cluster)   
   
## What is a Node?   
   
A node is a virtual or a physical machine that serves as a worker for running the applications.<br>   
It's recommended to have at least 3 nodes in a production environment.   
   
## What the master node is responsible for?   
   
The master coordinates all the workflows in the cluster:   
   
   
- Scheduling applications   
- Managing desired state   
- Rolling out new updates   
   
## Which command will list the nodes of the cluster?</code>   
   
`kubectl get nodes`   
   
## True or False? Every cluster must have 0 or more master nodes and at least 1 worker   
   
False. A Kubernetes cluster consists of at least 1 master and can have 0 workers (although that wouldn't be very useful...)   
   
## What are the components of the master node (aka control plane)?   
   
   
- API Server - the Kubernetes API. All cluster components communicate through it   
- Scheduler - assigns an application with a worker node it can run on   
- Controller Manager - cluster maintenance (replications, node failures, etc.)   
- etcd - stores cluster configuration   
   
## What are the components of a worker node (aka data plane)?   
   
   
- Kubelet - an agent responsible for node communication with the master.   
- Kube-proxy - load balancing traffic between app components   
- Container runtime - the engine runs the containers (Podman, Docker, ...)   
   
## Place the components on the right side of the image in the right place in the drawing<br>   
   
![](assets/images/2022-10-03-19-23-26.png)   
   
%   
   
![](assets/images/2022-10-03-19-23-44.png)   
   
## You are managing multiple Kubernetes clusters. How do you quickly change between the clusters using kubectl?   
   
`kubectl config use-context`   
   
## How do you prevent high memory usage in your Kubernetes cluster and possibly issues like memory leak and OOM?   
   
Apply requests and limits, especially on third party applications (where the uncertainty is even bigger)   
   
## Do you have experience with deploying a Kubernetes cluster? If so, can you describe the process in high-level?   
   
1. Create multiple instances you will use as Kubernetes nodes/workers. Create also an instance to act as the Master. The instances can be provisioned in a cloud or they can be virtual machines on bare metal hosts.   
2. Provision a certificate authority that will be used to generate TLS certificates for the different components of a Kubernetes cluster (kubelet, etcd, ...)   
3. Generate a certificate and private key for the different components   
4. Generate kubeconfigs so the different clients of Kubernetes can locate the API servers and authenticate.   
5. Generate encryption key that will be used for encrypting the cluster data   
6. Create an etcd cluster   
   
## Which command will list all the object types in a cluster?</code>   
   
`kubectl api-resources`   
   
## Explain what is a Pod   
   
A Pod is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.<br>   
Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.   
   
## Deploy a pod called "my-pod" using the nginx:alpine image   
   
`kubectl run my-pod --image=nginx:alpine --restart=Never`   
   
If you are a Kubernetes beginner you should know that this is not a common way to run Pods. The common way is to run a Deployment which in turn runs Pod(s).<br>   
In addition, Pods and/or Deployments are usually defined in files rather than executed directly using only the CLI arguments.   
   
## What are your thoughts on "Pods are not meant to be created directly"?   
   
Pods are usually indeed not created directly. You'll notice that Pods are usually created as part of another entities such as Deployments or ReplicaSets.<br>   
If a Pod dies, Kubernetes will not bring it back. This is why it's more useful for example to define ReplicaSets that will make sure that a given number of Pods will always run, even after a certain Pod dies.   
   
## How many containers can a pod contain?   
   
A pod can include multiple containers but in most cases it would probably be one container per pod.   
   
## What use cases exist for running multiple containers in a single pod?   
   
A web application with separate (= in their own containers) logging and monitoring components/adapters is one examples.<br>   
A CI/CD pipeline (using Tekton for example) can run multiple containers in one Pod if a Task contains multiple commands.   
   
## What are the possible Pod phases?   
   
   
- Running - The Pod bound to a node and at least one container is running   
- Failed - At least one container in the Pod terminated with a failure   
- Succeeded - Every container in the Pod terminated with success   
- Unknown - Pod's state could not be obtained   
- Pending - Containers are not yet running (Perhaps images are still being downloaded or the pod wasn't scheduled yet)   
   
## True or False? By default, pods are isolated. This means they are unable to receive traffic from any source   
   
False. By default, pods are non-isolated = pods accept traffic from any source.   
   
## True or False? The "Pending" phase means the Pod was not yet accepted by the Kubernetes cluster so the scheduler can't run it unless it's accepted   
   
False. "Pending" is after the Pod was accepted by the cluster, but the container can't run for different reasons like images not yet downloaded.   
   
## How to list the pods in the current namespace?</code>   
   
`kubectl get po`   
   
## How view all the pods running in all the namespaces?</code>   
   
`kubectl get pods --all-namespaces`   
   
## True or False? A single Pod can be split across multiple nodes</code>   
   
False. A single Pod can run on a single node.   
   
## How to delete a pod?</code>   
   
`kubectl delete pod pod_name`   
   
## How to find out on which node a certain pod is running?   
   
`kubectl get po -o wide`   
   
## What are "Static Pods"?   
   
   
- Managed directly by Kubelet on specific node   
- API server is not observing static Pods   
- For each static Pod there is a mirror Pod on kubernetes API server but it can't be managed from there   
   
Read more about it [here](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod)   
   
## True or False? A volume defined in Pod can be accessed by all the containers of that Pod   
   
True.   
   
## What happens when you run a Pod?   
   
1. Kubectl sends a request to the API server to create the Pod   
2. The Scheduler detects that there is an unassigned Pod (by monitoring the API server)   
3. The Scheduler chooses a node to assign the Pod to   
4. The Scheduler updates the API server about which node it chose   
5. Kubelet (which also monitors the API server) notices there is a Pod assigned to the same node on which it runs and that Pod isn't running   
6. Kubelet sends request to the container engine (e.g. Docker) to create and run the containers   
7. An update is sent by Kubelet to the API server (notifying it that the Pod is running)   
   
## How to confirm a container is running after running the command <code>kubectl run web --image nginxinc/nginx-unprivileged</code>   
   
   
- When you run `kubectl describe pods <POD_NAME>` it will tell whether the container is running:   
  `Status: Running`   
   
- Run a command inside the container: `kubectl exec web -- ls`   
   
## After running <code>kubectl run database --image mongo</code> you see the status is "CrashLoopBackOff". What could possibly went wrong and what do you do to confirm?   
   
"CrashLoopBackOff" means the Pod is starting, crashing, starting...and so it repeats itself.<br>   
There are many different reasons to get this error - lack of permissions, init-container misconfiguration, persistent volume connection issue, etc.   
   
One of the ways to check why it happened it to run `kubectl describe po <POD_NAME>` and having a look at the exit code   
   
```
 Last State:     Terminated
   Reason:       Error
   Exit Code:    100
```
   
   
Another way to check what's going on, is to run `kubectl logs <POD_NAME>`. This will provide us with the logs from the containers running in that Pod.   
   
## Explain the purpose of the following lines   
   
```
livenessProbe:
  exec:
    command:
    - cat
    - /appStatus
  initialDelaySeconds: 10
  periodSeconds: 5
```
   
   
These lines make use of `liveness probe`. It's used to restart a container when it reaches a non-desired state.<br>   
In this case, if the command `cat /appStatus` fails, Kubernetes will kill the container and will apply the restart policy. The `initialDelaySeconds: 10` means that Kubelet will wait 10 seconds before running the command/probe for the first time. From that point on, it will run it every 5 seconds, as defined with `periodSeconds`   
   
## Explain the purpose of the following lines   
   
```
readinessProbe:
      tcpSocket:
        port: 2017
      initialDelaySeconds: 15
      periodSeconds: 20
```
   
   
They define a readiness probe where the Pod will not be marked as "Ready" before it will be possible to connect to port 2017 of the container. The first check/probe will start after 15 seconds from the moment the container started to run and will continue to run the check/probe every 20 seconds until it will manage to connect to the defined port.   
   
## What does the "ErrImagePull" status of a Pod means?   
   
It wasn't able to pull the image specified for running the container(s). This can happen if the client didn't authenticated for example.<br>   
More details can be obtained with `kubectl describe po <POD_NAME>`.   
   
## What happens when you delete a Pod?   
   
1. The `TERM` signal is sent to kill the main processes inside the containers of the given Pod   
2. Each container is given a period of 30 seconds to shut down the processes gracefully   
3. If the grace period expires, the `KILL` signal is used to kill the processes forcefully and the containers as well   
   
## Explain liveness probes   
   
Liveness probes is a useful mechanism used for restarting the container when a certain check/probe, the user has defined, fails.<br>   
For example, the user can define that the command `cat /app/status` will run every X seconds and the moment this command fails, the container will be restarted.   
   
You can read more about it in [kubernetes.io](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes)   
   
## Explain readiness probes   
   
readiness probes used by Kubelet to know when a container is ready to start running, accepting traffic.<br>   
For example, a readiness probe can be to connect port 8080 on a container. Once Kubelet manages to connect it, the Pod is marked as ready   
   
You can read more about it in [kubernetes.io](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes)   
   
## How readiness probe status affect Services when they are combined?   
   
Only containers whose state set to Success will be able to receive requests sent to the Service.   
   
## Why it's common to have only one container per Pod in most cases?   
   
One reason is that it makes it harder to scale when you need to scale only one of the containers in a given Pod.   
   
## True or False? Once a Pod is assisgned to a worker node, it will only run on that node, even if it fails at some point and spins up a new Pod   
   
True.   
   
## True or False? Each Pod, when created, gets its own public IP address   
   
False. Each Pod gets an IP address but an internal one and not publicly accessible.   
   
To make a Pod externally accessible, we need to use an object called Service in Kubernetes.   
   
## How to check to which worker node the pods were scheduled to?   
   
`kubectl get pods -o wide`   
   
## What is a "Deployment" in Kubernetes?   
   
A Kubernetes Deployment is used to tell Kubernetes how to create or modify instances of the pods that hold a containerized application.   
Deployments can scale the number of replica pods, enable rollout of updated code in a controlled manner, or roll back to an earlier deployment version if necessary.   
   
A Deployment is a declarative statement for the desired state for Pods and Replica Sets.   
   
## How to create a deployment?</code>   
   
`kubectl create deployment my_first_deployment --image=nginx:alpine`   
   
OR   
   
```
cat << EOF | kubectl create -f -
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:alpine
EOF
```
   
   
## How to verify a deployment was created?</code>   
   
`kubectl get deployments`   
   
This command lists all the Deployment objects created and exist in the cluster. It doesn't mean the deployments are readt and running. This can be checked with the "READY" and "AVAILABLE" columns.   
   
## How to edit a deployment?</code>   
   
kubectl edit deployment some-deployment   
   
## What happens after you edit a deployment and change the image?   
   
The pod will terminate and another, new pod, will be created.   
   
Also, when looking at the replicaset, you'll see the old replica doesn't have any pods and a new replicaset is created.   
   
## How to delete a deployment?   
   
One way is by specifying the deployment name: `kubectl delete deployment [deployment_name]`<br>   
Another way is using the deployment configuration file: `kubectl delete -f deployment.yaml`   
   
## What happens when you delete a deployment?   
   
The pod related to the deployment will terminate and the replicaset will be removed.   
   
## What happens behind the scenes when you create a Deployment object?   
   
The following occurs when you run `kubectl create deployment some_deployment --image=nginx`   
   
1. HTTP request sent to kubernetes API server on the cluster to create a new deployment   
2. A new Pod object is created and scheduled to one of the workers nodes   
3. Kublet on the worker node notices the new Pod and instructs the Container runtime engine to pull the image from the registry   
4. A new container is created using the image that was just pulled   
   
## How make an app accessible on private or external network?   
   
Using a Service.   
   
## Can you use a Deployment for stateful applications?   
   
## What is a Service in Kubernetes?   
   
"An abstract way to expose an application running on a set of Pods as a network service." - read more [here](https://kubernetes.io/docs/concepts/services-networking/service)<br>   
   
In simpler words, it allows you to add an internal or external connectivity to a certain application running in a container.   
   
## How to create a service for an existing deployment called "alle" on port 8080 so the Pod(s) accessible via a Load Balancer?   
   
The imperative way:   
   
`kubectl expose deployment alle --type=LoadBalancer --port 8080`   
   
## An internal load balancer in Kubernetes is called <code>\_**\_</code> and an external load balancer is called <code>\_\_**</code>   
   
An internal load balancer in Kubernetes is called Service and an external load balancer is Ingress   
   
## True or False? The lifecycle of Pods and Services isn't connected so when a Pod dies, the Service still stays   
   
True   
   
## After creating a service, how to check it was created?   
   
`kubectl get svc`   
   
## What Service types are there?   
   
   
- ClusterIP   
- NodePort   
- LoadBalancer   
- ExternalName   
   
More on this topic [here](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)   
   
## How Service and Deployment are connected?   
   
The truth is they aren't connected. Service points to Pod(s) directly, without connecting to the Deployment in any way.   
   
## What are important steps in defining/adding a Service?   
   
1. Making sure that targetPort of the Service is matching the containerPort of the Pod   
2. Making sure that selector matches at least one of the Pod's labels   
   
## What is the default service type in Kubernetes and what is it used for?   
   
The default is ClusterIP and it's used for exposing a port internally. It's useful when you want to enable internal communication between Pods and prevent any external access.   
   
## How to get information on a certain service?   
   
`kubctl describe service <SERVICE_NAME>`   
   
It's more common to use `kubectl describe svc ...`   
   
## What the following command does?   
   
```
kubectl expose rs some-replicaset --name=replicaset-svc --target-port=2017 --type=NodePort
```
   
   
It exposes a ReplicaSet by creating a service called 'replicaset-svc'. The exposed port is 2017 (this is the port used by the application) and the service type is NodePort which means it will be reachable externally.   
   
## True or False? the target port, in the case of running the following command, will be exposed only on one of the Kubernetes cluster nodes but it will routed to all the pods   
   
```
kubectl expose rs some-replicaset --name=replicaset-svc --target-port=2017 --type=NodePort
```
   
   
False. It will be exposed on every node of the cluster and will be routed to one of the Pods (which belong to the ReplicaSet)   
   
## How to verify that a certain service configured to forward the requests to a given pod   
   
Run `kubectl describe service` and see if the IPs from "Endpoints" match any IPs from the output of `kubectl get pod -o wide`   
   
## Explain what will happen when running apply on the following block   
   
```
apiVersion: v1
kind: Service
metadata:
  name: some-app
spec:
  type: NodePort
  ports:
  - port: 8080
    nodePort: 2017
    protocol: TCP
  selector:
    type: backend
    service: some-app
```
   
   
It creates a new Service of the type "NodePort" which means it can be used for internal and external communication with the app.<br>   
The port of the application is 8080 and the requests will forwarded to this port. The exposed port is 2017. As a note, this is not a common practice, to specify the nodePort.<br>   
The port used TCP (instead of UDP) and this is also the default so you don't have to specify it.<br>   
The selector used by the Service to know to which Pods to forward the requests. In this case, Pods with the label "type: backend" and "service: some-app".<br>   
   
## How to turn the following service into an external one?   
   
```
spec:
  selector:
    app: some-app
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
```
   
   
Adding `type: LoadBalancer` and `nodePort`   
   
```
spec:
  selector:
    app: some-app
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
      nodePort: 32412
```
   
   
## What would you use to route traffic from outside the Kubernetes cluster to services within a cluster?   
   
Ingress   
   
## True or False? When "NodePort" is used, "ClusterIP" will be created automatically?   
   
True   
   
## When would you use the "LoadBalancer" type   
   
Mostly when you would like to combine it with cloud provider's load balancer   
   
## How would you map a service to an external address?   
   
Using the 'ExternalName' directive.   
   
## Describe in detail what happens when you create a service   
   
1. Kubectl sends a request to the API server to create a Service   
2. The controller detects there is a new Service   
3. Endpoint objects created with the same name as the service, by the controller   
4. The controller is using the Service selector to identify the endpoints   
5. kube-proxy detects there is a new endpoint object + new service and adds iptables rules to capture traffic to the Service port and redirect it to endpoints   
6. kube-dns detects there is a new Service and adds the container record to the dns server   
   
## How to list the endpoints of a certain app?   
   
`kubectl get ep <name>`   
   
## How can you find out information on a Service related to a certain Pod if all you can use is <code>kubectl exec <POD_NAME> -- </code>   
   
You can run `kubectl exec <POD_NAME> -- env` which will give you a couple environment variables related to the Service.<br>   
Variables such as `[SERVICE_NAME]_SERVICE_HOST`, `[SERVICE_NAME]_SERVICE_PORT`, ...   
   
## Describe what happens when a container tries to connect with its corresponding Service for the first time. Explain who added each of the components you include in your description   
   
   
- The container looks at the nameserver defined in /etc/resolv.conf   
- The container queries the nameserver so the address is resolved to the Service IP   
- Requests sent to the Service IP are forwarded with iptables rules (or other chosen software) to the endpoint(s).   
   
Explanation as to who added them:   
   
   
- The nameserver in the container is added by kubelet during the scheduling of the Pod, by using kube-dns   
- The DNS record of the service is added by kube-dns during the Service creation   
- iptables rules are added by kube-proxy during Endpoint and Service creation   
   
## Describe in high level what happens when you run <code>kubctl expose deployment remo --type=LoadBalancer --port 8080</code>   
   
1. Kubectl sends a request to Kubernetes API to create a Service object   
2. Kubernetes asks the cloud provider (e.g. AWS, GCP, Azure) to provision a load balancer   
3. The newly created load balancer forwards incoming traffic to relevant worker node(s) which forwards the traffic to the relevant containers   
   
## After creating a service that forwards incoming external traffic to the containerized application, how to make sure it works?   
   
You can run `curl <SERIVCE IP>:<SERVICE PORT>` to examine the output.   
   
## What is Ingress?   
   
From Kubernetes docs: "Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource."   
   
Read more [here](https://kubernetes.io/docs/concepts/services-networking/ingress/)   
   
## Complete the following configuration file to make it Ingress   
   
```
metadata:
  name: someapp-ingress
spec:
```
   
   
There are several ways to answer this question.   
   
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: someapp-ingress
spec:
  rules:
  - host: my.host
    http:
      paths:
      - backend:
          serviceName: someapp-internal-service
          servicePort: 8080
```
   
   
## Explain the meaning of "http", "host" and "backend" directives   
   
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: someapp-ingress
spec:
  rules:
  - host: my.host
    http:
      paths:
      - backend:
          serviceName: someapp-internal-service
          servicePort: 8080
```
   
   
host is the entry point of the cluster so basically a valid domain address that maps to cluster's node IP address<br>   
the http line used for specifying that incoming requests will be forwarded to the internal service using http.<br>   
backend is referencing the internal service (serviceName is the name under metadata and servicePort is the port under the ports section).   
   
## Why using a wildcard in ingress host may lead to issues?   
   
The reason you should not wildcard value in a host (like `- host: *`) is because you basically tell your Kubernetes cluster to forward all the traffic to the container where you used this ingress. This may cause the entire cluster to go down.   
   
## What is Ingress Controller?   
   
An implementation for Ingress. It's basically another pod (or set of pods) that does evaluates and processes Ingress rules and this it manages all the redirections.   
   
There are multiple Ingress Controller implementations (the one from Kubernetes is Kubernetes Nginx Ingress Controller).   
   
## What are some use cases for using Ingress?   
   
   
- Multiple sub-domains (multiple host entries, each with its own service)   
- One domain with multiple services (multiple paths where each one is mapped to a different service/application)   
   
## How to list Ingress in your namespace?   
   
kubectl get ingress   
   
## What is Ingress Default Backend?   
   
It specifies what do with an incoming request to the Kubernetes cluster that isn't mapped to any backend (= no rule to for mapping the request to a service). If the default backend service isn't defined, it's recommended to define so users still see some kind of message instead of nothing or unclear error.   
   
## How to configure a default backend?   
   
Create Service resource that specifies the name of the default backend as reflected in `kubectl describe ingress ...` and the port under the ports section.   
   
## How to configure TLS with Ingress?   
   
Add tls and secretName entries.   
   
```
spec:
  tls:
  - hosts:
    - some_app.com
    secretName: someapp-secret-tls
```
   
   
## True or False? When configuring Ingress with TLS, the Secret component must be in the same namespace as the Ingress component   
   
True   
   
## Which Kubernetes concept would you use to control traffic flow at the IP address or port level?   
   
Network Policies   
   
## How to scale an application (deplyoment) so it runs more than one instance of the application?   
   
To run two instances of the applicaation?   
   
`kubectl scale deployment <DEPLOYMENT_NAME> --replicas=2`   
   
You can speciy any other number, given that your application knows how to scale.   
   
## What is the purpose of ReplicaSet?   
   
[kubernetes.io](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset): "A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods."   
   
In simpler words, a ReplicaSet will ensure the specified number of Pods replicas is running for a selected Pod. If there are more Pods than defined in the ReplicaSet, some will be removed. If there are less than what is defined in the ReplicaSet then, then more replicas will be added.   
   
## What the following block of lines does?   
   
```
spec:
  replicas: 2
  selector:
    matchLabels:
      type: backend
  template:
    metadata:
      labels:
        type: backend
    spec:
      containers:
      - name: httpd-yup
        image: httpd
```
   
   
It defines a replicaset for Pods whose type is set to "backend" so at any given point of time there will be 2 concurrent Pods running.   
   
## What will happen when a Pod, created by ReplicaSet, is deleted directly with <code>kubectl delete po ...</code>?   
   
The ReplicaSet will create a new Pod in order to reach the desired number of replicas.   
   
## True or False? If a ReplicaSet defines 2 replicas but there 3 Pods running matching the ReplicaSet selector, it will do nothing   
   
False. It will terminate one of the Pods to reach the desired state of 2 replicas.   
   
## Describe the sequence of events in case of creating a ReplicaSet   
   
   
- The client (e.g. kubectl) sends a request to the API server to create a ReplicaSet   
- The Controller detects there is a new event requesting for a ReplicaSet   
- The controller creates new Pod definitions (the exact number depends on what is defined in the ReplicaSet definition)   
- The scheduler detects unassigned Pods and decides to which nodes to assign the Pods. This information sent to the API server   
- Kubelet detects that two Pods were assigned to the node it's running on (as it constantly watching the API server)   
- Kubelet sends requests to the container engine, to create the containers that are part of the Pod   
- Kubelet sends a request to the API server to notify it the Pods were created   
   
## How to list ReplicaSets in the current namespace?   
   
kubectl get rs   
   
## Is it possible to delete ReplicaSet without deleting the Pods it created?   
   
Yes, with `--cascase=false`.   
   
`kubectl delete -f rs.yaml --cascade=false`   
   
## What is the default number of replicas if not explicitly specified?   
   
1   
   
## What the following output of <code>kubectl get rs</code> means?   
   
NAME DESIRED CURRENT READY AGE   
web 2 2 0 2m23s   
   
The replicaset `web` has 2 replicas. It seems that the containers inside the Pod(s) are not yet running since the value of READY is 0. It might be normal since it takes time for some containers to start running and it might be due to an error. Running `kubectl describe po POD_NAME` or `kubectl logs POD_NAME` can give us more information.   
   
## You run <code>kubectl get rs</code> and while DESIRED is set to 2, you see that READY is set to 0. What are some possible reasons for it to be 0?   
   
   
- Images are still being pulled   
- There is an error and the containers can't reach the state "Running"   
   
## True or False? Pods specified by the selector field of ReplicaSet must be created by the ReplicaSet itself   
   
False. The Pods can be already running and initially they can be created by any object. It doesn't matter for the ReplicaSet and not a requirement for it to acquire and monitor them.   
   
## True or False? In case of a ReplicaSet, if Pods specified in the selector field don't exists, the ReplicaSet will wait for them to run before doing anything   
   
False. It will take care of running the missing Pods.   
   
## In case of a ReplicaSet, Which field is mandatory in the spec section?   
   
The field `template` in spec section is mandatory. It's used by the ReplicaSet to create new Pods when needed.   
   
## You've created a ReplicaSet, how to check whether the ReplicaSet found matching Pods or it created new Pods?   
   
`kubectl describe rs <ReplicaSet Name>`   
   
It will be visible under `Events` (the very last lines)   
   
## True or False? Deleting a ReplicaSet will delete the Pods it created   
   
True (and not only the Pods but anything else it created).   
   
## True or False? Removing the label from a Pod that is used by ReplicaSet to match Pods, will cause the ReplicaSet to create a new Pod   
   
True. When the label, used by a ReplicaSet in the selector field, removed from a Pod, that Pod no longer controlled by the ReplicaSet and the ReplicaSet will create a new Pod to compensate for the one it "lost".   
   
## How to scale a deployment to 8 replicas?</code>   
   
kubectl scale deploy <DEPLOYMENT_NAME> --replicas=8   
   
## ReplicaSets are running the moment the user executed the command to create them (like <code>kubectl create -f rs.yaml</code>)   
   
False. It can take some time, depends on what exactly you are running. To see if they are up and running, run `kubectl get rs` and watch the 'READY' column.   
   
## How to expose a ReplicaSet as a new service?   
   
`kubectl expose rs <ReplicaSet Name> --name=<Service Name> --target-port=<Port to expose> --type=NodePort`   
   
Few notes:   
   
   
- the target port depends on which port the app is using in the container   
- type can be different and doesn't has to be specifically "NodePort"   
   
## What's the diffence between a ReplicaSet and DaemonSet?   
   
A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time.   
A DaemonSet ensures that all Nodes run a copy of a Pod.   
   
## StatefulSet   
   
## Explain StatefulSet   
   
StatefulSet is the workload API object used to manage stateful applications. Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.[Learn more](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)   
   
## What is a volume in regards to Kubernetes?   
   
A directory accessible by the containers inside a certain Pod. The mechanism responsible for creating the directory and managing it, ... is mainly depends on the volume type.   
   
## Which problems volumes in Kubernetes solve?   
   
1. Sharing files between containers running in the same Pod   
2. Storage in containers is ephemeral - it usually doesn't last for long. For example, when a container crashes, you lose all on-disk data.   
   
## Explain ephemeral volume types vs. persistent volumes in regards to Pods   
   
Ephemeral volume types have the lifetime of a pod as opposed to persistent volumes which exist beyond the lifetime of a Pod.   
   
## Explain Network Policies   
   
[kubernetes.io](https://kubernetes.io/docs/concepts/services-networking/network-policies): "NetworkPolicies are an application-centric construct which allow you to specify how a pod is allowed to communicate with various network "entities"..."   
   
In simpler words, Network Policies specify how pods are allowed/disallowed to communicate with each other and/or other network endpoints.   
   
## What are some use cases for using Network Policies?   
   
   
- Security: You want to prevent from everyone to communicate with a certain pod for security reasons   
- Controlling network traffic: You would like to deny network flow between two specific nodes   
   
## True or False? If no network policies are applied to a pod, then no connections to or from it are allowed   
   
False. By default pods are non-isolated.   
   
## In case of two pods, if there is an egress policy on the source denining traffic and ingress policy on the destination that allows traffic then, traffic will be allowed or denied?   
   
Denied. Both source and destination policies has to allow traffic for it to be allowed.   
   
## Which parts a configuration file has?   
   
It has three main parts:   
   
1. Metadata   
2. Specification   
3. Status (this automatically generated and added by Kubernetes)   
   
## What is the format of a configuration file?   
   
YAML   
   
## How to get latest configuration of a deployment?   
   
`kubectl get deployment [deployment_name] -o yaml`   
   
## Where Kubernetes cluster stores the cluster state?   
   
etcd   
   
## What is etcd?   
   
etcd is an open source distributed key-value store used to hold and manage the critical information that distributed systems need to keep running.[Read more](https://www.redhat.com/en/topics/containers/what-is-etcd)   
   
## True or False? Etcd holds the current status of any kubernetes component   
   
True   
   
## True or False? The API server is the only component which communicates directly with etcd   
   
True   
   
## True or False? application data is not stored in etcd   
   
True   
   
## Why etcd? Why not some SQL or NoSQL database?   
   
## What are namespaces?   
   
Namespaces allow you split your cluster into virtual clusters where you can group your applications in a way that makes sense and is completely separated from the other groups (so you can for example create an app with the same name in two different namespaces)   
   
<a name="namespaces-use-cases"></a>   
   
## Why to use namespaces? What is the problem with using one default namespace?   
   
When using the default namespace alone, it becomes hard over time to get an overview of all the applications you manage in your cluster. Namespaces make it easier to organize the applications into groups that makes sense, like a namespace of all the monitoring applications and a namespace for all the security applications, etc.   
   
Namespaces can also be useful for managing Blue/Green environments where each namespace can include a different version of an app and also share resources that are in other namespaces (namespaces like logging, monitoring, etc.).   
   
Another use case for namespaces is one cluster, multiple teams. When multiple teams use the same cluster, they might end up stepping on each others toes. For example if they end up creating an app with the same name it means one of the teams overridden the app of the other team because there can't be too apps in Kubernetes with the same name (in the same namespace).   
   
## True or False? When a namespace is deleted all resources in that namespace are not deleted but moved to another default namespace   
   
False. When a namespace is deleted, the resources in that namespace are deleted as well.   
   
## What special namespaces are there by default when creating a Kubernetes cluster?   
   
   
- default   
- kube-system   
- kube-public   
- kube-node-lease   
   
## What can you find in kube-system namespace?   
   
   
- Master and Kubectl processes   
- System processes   
   
## How to list all namespaces?</code>   
   
`kubectl get namespaces`   
   
## What kube-public contains?   
   
   
- A configmap, which contains cluster information   
- Publicely accessible data   
   
## How to get the name of the current namespace?</code>   
   
kubectl config view | grep namespace   
   
## What kube-node-lease contains?   
   
It holds information on hearbeats of nodes. Each node gets an object which holds information about its availability.   
   
## How to create a namespace?   
   
One way is by running `kubectl create namespace [NAMESPACE_NAME]`   
   
Another way is by using namespace configuration file:   
   
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: some-cofngimap
  namespace: some-namespace
```
   
   
## What default namespace contains?   
   
Any resource you create while using Kubernetes.   
   
## True or False? With namespaces you can limit the resources consumed by the users/teams   
   
True. With namespaces you can limit CPU, RAM and storage usage.   
   
## How to switch to another namespace? In other words how to change active namespace?</code>   
   
`kubectl config set-context --current --namespace=some-namespace` and validate with `kubectl config view --minify | grep namespace:`   
   
OR   
   
`kubens some-namespace`   
   
## What is Resource Quota?</code>   
   
Resource quota provides constraints that limit aggregate resource consumption per namespace. It can limit the quantity of objects that can be created in a namespace by type, as well as the total amount of compute resources that may be consumed by resources in that namespace.   
   
## How to create a Resource Quota?</code>   
   
kubectl create quota some-quota --hard-cpu=2,pods=2   
   
## Which resources are accessible from different namespaces?</code>   
   
Service.   
   
## Let's say you have three namespaces: x, y and z. In x namespace you have a ConfigMap referencing service in z namespace. Can you reference the ConfigMap in x namespace from y namespace?</code>   
   
No, you would have to create separate namespace in y namespace.   
   
## Which service and in which namespace the following file is referencing?   
   
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: some-configmap
data:
  some_url: samurai.jack
```
   
   
It's referencing the service "samurai" in the namespace called "jack".   
   
## Which components can't be created within a namespace?</code>   
   
Volume and Node.   
   
## How to list all the components that bound to a namespace?</code>   
   
`kubectl api-resources --namespaced=true`   
   
## How to create components in a namespace?</code>   
   
One way is by specifying --namespace like this: `kubectl apply -f my_component.yaml --namespace=some-namespace`   
Another way is by specifying it in the YAML itself:   
   
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: some-configmap
  namespace: some-namespace
```
   
   
and you can verify with: `kubectl get configmap -n some-namespace`   
   
## How to execute the command "ls" in an existing pod?</code>   
   
kubectl exec some-pod -it -- ls   
   
## How to create a service that exposes a deployment?</code>   
   
kubectl expose deploy some-deployment --port=80 --target-port=8080   
   
## How to create a pod and a service with one command?</code>   
   
kubectl run nginx --image=nginx --restart=Never --port 80 --expose   
   
## Describe in detail what the following command does <code>kubectl create deployment kubernetes-httpd --image=httpd</code>   
   
## Why to create kind deployment, if pods can be launched with replicaset?   
   
## How to get list of resources which are not bound to a specific namespace?</code>   
   
kubectl api-resources --namespaced=false   
   
## How to delete all pods whose status is not "Running"?</code>   
   
kubectl delete pods --field-selector=status.phase!='Running'   
   
## What <code>kubectl logs [pod-name]</code> command does?   
   
Print the logs for a container in a pod.   
   
## What <code>kubectl describe pod [pod name] does?</code> command does?   
   
Show details of a specific resource or group of resources.   
   
## How to display the resources usages of pods?   
   
kubectl top pod   
   
## What <code>kubectl get componentstatus</code> does?   
   
Outputs the status of each of the control plane components.   
   
## What is Minikube?   
   
Minikube is a lightweight Kubernetes implementation. It create a local virtual machine and deploys a simple (single node) cluster.   
   
## How do you monitor your Kubernetes?   
   
## You suspect one of the pods is having issues, what do you do?   
   
Start by inspecting the pods status. we can use the command `kubectl get pods` (--all-namespaces for pods in system namespace)<br>   
   
If we see "Error" status, we can keep debugging by running the command `kubectl describe pod [name]`. In case we still don't see anything useful we can try stern for log tailing.<br>   
   
In case we find out there was a temporary issue with the pod or the system, we can try restarting the pod with the following `kubectl scale deployment [name] --replicas=0`<br>   
   
Setting the replicas to 0 will shut down the process. Now start it with `kubectl scale deployment [name] --replicas=1`   
   
## What the Kubernetes Scheduler does?   
   
## What happens to running pods if if you stop Kubelet on the worker nodes?   
   
## What happens what pods are using too much memory? (more than its limit)   
   
They become candidates to for termination.   
   
## Describe how roll-back works   
   
## True or False? Memory is a compressible resource, meaning that when a container reach the memory limit, it will keep running   
   
False. CPU is a compressible resource while memory is a non compressible resource - once a container reached the memory limit, it will be terminated.   
   
## What is an Operator?   
   
Explained [here](https://kubernetes.io/docs/concepts/extend-kubernetes/operator)   
   
"Operators are software extensions to Kubernetes that make use of custom resources to manage applications and their components. Operators follow Kubernetes principles, notably the control loop."   
   
In simpler words, you can think about an operator as a custom control loop in Kubernetes.   
   
## Why do we need Operators?   
   
The process of managing stateful applications in Kubernetes isn't as straightforward as managing stateless applications where reaching the desired status and upgrades are both handled the same way for every replica. In stateful applications, upgrading each replica might require different handling due to the stateful nature of the app, each replica might be in a different status. As a result, we often need a human operator to manage stateful applications. Kubernetes Operator is suppose to assist with this.   
   
This also help with automating a standard process on multiple Kubernetes clusters   
   
## What components the Operator consists of?   
   
1. CRD (Custom Resource Definition) - You are fanmiliar with Kubernetes resources like Deployment, Pod, Service, etc. CRD is also a resource, but one that you or the developer the operator defines.   
2. Controller - Custom control loop which runs against the CRD   
   
## Explain CRD   
   
CRD is Custom Resource Definitions. It's custom Kubernetes component which extends K8s API.   
   
TODO(abregman): add more info.   
   
## How Operator works?   
   
It uses the control loop used by Kubernetes in general. It watches for changes in the application state. The difference is that is uses a custom control loop.   
   
In addition, it also makes use of CRD's (Custom Resources Definitions) so basically it extends Kubernetes API.   
   
## True or False? Kubernetes Operator used for stateful applications   
   
True   
   
## Explain what is the OLM (Operator Lifecycle Manager) and what is it used for   
   
## What is the Operator Framework?   
   
open source toolkit used to manage k8s native applications, called operators, in an automated and efficient way.   
   
## What components the Operator Framework consists of?   
   
1. Operator SDK - allows developers to build operators   
2. Operator Lifecycle Manager - helps to install, update and generally manage the lifecycle of all operators   
3. Operator Metering - Enables usage reporting for operators that provide specialized services   
4.   
   
## Describe in detail what is the Operator Lifecycle Manager   
   
It's part of the Operator Framework, used for managing the lifecycle of operators. It basically extends Kubernetes so a user can use a declarative way to manage operators (installation, upgrade, ...).   
   
## What openshift-operator-lifecycle-manager namespace includes?   
   
It includes:   
   
   
- catalog-operator - Resolving and installing ClusterServiceVersions the resource they specify.   
- olm-operator - Deploys applications defined by ClusterServiceVersion resource   
   
## What is kubconfig? What do you use it for?   
   
A kubeconfig file is a file used to configure access to Kubernetes when used in conjunction with the kubectl commandline tool (or other clients).   
Use kubeconfig files to organize information about clusters, users, namespaces, and authentication mechanisms.   
   
## Would you use Helm, Go or something else for creating an Operator?   
   
Depends on the scope and maturity of the Operator. If it mainly covers installation and upgrades, Helm might be enough. If you want to go for Lifecycle management, insights and auto-pilot, this is where you'd probably use Go.   
   
## Are there any tools, projects you are using for building Operators?   
   
This one is based more on a personal experience and taste...   
   
   
- Operator Framework   
- Kubebuilder   
- Controller Runtime   
  ...   
   
## Explain Kubernetes Secrets   
   
Secrets let you store and manage sensitive information (passwords, ssh keys, etc.)   
   
## How to create a Secret from a key and value?   
   
kubectl create secret generic some-secret --from-literal=password='donttellmypassword'   
   
## How to create a Secret from a file?   
   
kubectl create secret generic some-secret --from-file=/some/file.txt   
   
## What <code>type: Opaque</code> in a secret file means? What other types are there?   
   
Opaque is the default type used for key-value pairs.   
   
## True or False? storing data in a Secret component makes it automatically secured   
   
False. Some known security mechanisms like "encryption" aren't enabled by default.   
   
## What is the problem with the following Secret file:   
   
```
apiVersion: v1
kind: Secret
metadata:
    name: some-secret
type: Opaque
data:
    password: mySecretPassword
```
   
   
Password isn't encrypted.   
You should run something like this: `echo -n 'mySecretPassword' | base64` and paste the result to the file instead of using plain-text.   
   
## How to create a Secret from a configuration file?   
   
`kubectl apply -f some-secret.yaml`   
   
## What the following in Deployment configuration file means?   
   
```
spec:
  containers:
    - name: USER_PASSWORD
      valueFrom:
        secretKeyRef:
          name: some-secret
          key: password
```
   
   
USER_PASSWORD environment variable will store the value from password key in the secret called "some-secret"   
In other words, you reference a value from a Kubernetes Secret.   
   
## True or False? Kubernetes provides data persistence out of the box, so when you restart a pod, data is saved   
   
False   
   
## Explain "Persistent Volumes". Why do we need it?   
   
Persistent Volumes allow us to save data so basically they provide storage that doesn't depend on the pod lifecycle.   
   
## True or False? Persistent Volume must be available to all nodes because the pod can restart on any of them   
   
True   
   
## What types of persistent volumes are there?   
   
   
- NFS   
- iSCSI   
- CephFS   
- ...   
   
## What is PersistentVolumeClaim?   
   
## Explain Volume Snapshots   
   
Volume snapshots let you create a copy of your volume at a specific point in time.   
   
## True or False? Kubernetes manages data persistence   
   
False   
   
## Explain Storage Classes   
   
## Explain "Dynamic Provisioning" and "Static Provisioning"   
   
The main difference relies on the moment when you want to configure storage. For instance, if you need to pre-populate data in a volume, you choose static provisioning. Whereas, if you need to create volumes on demand, you go for dynamic provisioning.   
   
## Explain Access Modes   
   
## What is CSI Volume Cloning?   
   
## Explain "Ephemeral Volumes"   
   
## What types of ephemeral volumes Kubernetes supports?   
   
## What is Reclaim Policy?   
   
## What reclaim policies are there?   
   
   
- Retain   
- Recycle   
- Delete   
   
## What is RBAC?   
   
RBAC in Kubernetes is the mechanism that enables you to configure fine-grained and specific sets of permissions that define how a given user, or group of users, can interact with any Kubernetes object in cluster, or in a specific Namespace of cluster.   
   
## Explain the <code>Role</code> and <code>RoleBinding"</code> objects   
   
## What is the difference between <code>Role</code> and <code>ClusterRole</code> objects?   
   
The difference between them is that a Role is used at a namespace level whereas a ClusterRole is for the entire cluster.   
   
## Explain what are "Service Accounts" and in which scenario would use create/use one   
   
[Kubernetes.io](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account): "A service account provides an identity for processes that run in a Pod."   
   
An example of when to use one:   
You define a pipeline that needs to build and push an image. In order to have sufficient permissions to build an push an image, that pipeline would require a service account with sufficient permissions.   
   
## What happens you create a pod and you DON'T specify a service account?   
   
The pod is automatically assigned with the default service account (in the namespace where the pod is running).   
   
## Explain how Service Accounts are different from User Accounts   
   
   
- User accounts are global while Service accounts unique per namespace   
- User accounts are meant for humans or client processes while Service accounts are for processes which run in pods   
   
## How to list Service Accounts?   
   
`kubectl get serviceaccounts`   
   
## Explain "Security Context"   
   
[kubernetes.io](https://kubernetes.io/docs/tasks/configure-pod-container/security-context): "A security context defines privilege and access control settings for a Pod or Container."   
   
## Explain the sidecar container pattern   
   
The sidecar pattern is a single-node pattern made up of two containers. The first is the application container. It contains the core logic for the application.   
Without this container, the application would not exist. In addition to the application container, there is a sidecar container.   
   
## Explain what is CronJob and what is it used for   
   
A CronJob creates Jobs on a repeating schedule. One CronJob object is like one line of a crontab (cron table) file. It runs a job periodically on a given schedule, written in Cron format.   
   
## What possible issue can arise from using the following spec and how to fix it?   
   
```
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: some-cron-job
spec:
  schedule: '*/1 * * * *'
  startingDeadlineSeconds: 10
  concurrencyPolicy: Allow
```
   
   
If the cron job fails, the next job will not replace the previous one due to the "concurrencyPolicy" value which is "Allow". It will keep spawning new jobs and so eventually the system will be filled with failed cron jobs.   
To avoid such problem, the "concurrencyPolicy" value should be either "Replace" or "Forbid".   
   
## What issue might arise from using the following CronJob and how to fix it?   
   
```
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: "some-cron-job"
spec:
  schedule: '*/1 * * * *'
jobTemplate:
  spec:
    template:
      spec:
      restartPolicy: Never
      concurrencyPolicy: Forbid
      successfulJobsHistoryLimit: 1
      failedJobsHistoryLimit: 1
```
   
   
The following lines placed under the template:   
   
```
concurrencyPolicy: Forbid
successfulJobsHistoryLimit: 1
failedJobsHistoryLimit: 1
```
   
   
As a result this configuration isn't part of the cron job spec hence the cron job has no limits which can cause issues like OOM and potentially lead to API server being down.<br>   
To fix it, these lines should placed in the spec of the cron job, above or under the "schedule" directive in the above example.   
   
## Explain Imperative Management vs. Declarative Management   
   
## Explain what Kubernetes Service Discovery means   
   
## You have one Kubernetes cluster and multiple teams that would like to use it. You would like to limit the resources each team consumes in the cluster. Which Kubernetes concept would you use for that?   
   
Namespaces will allow to limit resources and also make sure there are no collisions between teams when working in the cluster (like creating an app with the same name).   
   
## What Kube Proxy does?   
   
Kube Proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept   
   
## What "Resources Quotas" are used for and how?   
   
## Explain ConfigMap   
   
Separate configuration from pods.   
It's good for cases where you might need to change configuration at some point but you don't want to restart the application or rebuild the image so you create a ConfigMap and connect it to a pod but externally to the pod.   
   
Overall it's good for:   
   
   
- Sharing the same configuration between different pods   
- Storing external to the pod configuration   
   
## How to use ConfigMaps?   
   
1. Create it (from key&value, a file or an env file)   
2. Attach it. Mount a configmap as a volume   
   
## True or False? Sensitive data, like credentials, should be stored in a ConfigMap   
   
False. Use secret.   
   
## Explain "Horizontal Pod Autoscaler"   
   
In Kubernetes, a HorizontalPodAutoscaler automatically updates a workload resource with the aim of automatically scaling the workload to match demand.   
   
## When you delete a pod, is it deleted instantly? (a moment after running the command)   
   
## What does being cloud-native mean?   
   
The term cloud native refers to the concept of building and running applications to take advantage of the distributed computing offered by the cloud delivery model.   
   
## Explain the pet and cattle approach of infrastructure with respect to kubernetes   
   
## Describe how you one proceeds to run a containerized web app in K8s, which should be reachable from a public URL.   
   
## How would you troubleshoot your cluster if some applications are not reachable any more?   
   
## Describe what CustomResourceDefinitions there are in the Kubernetes world? What they can be used for?   
   
## How does scheduling work in kubernetes?   
   
The control plane component kube-scheduler asks the following questions,   
   
1. What to schedule? It tries to understand the pod-definition specifications   
2. Which node to schedule? It tries to determine the best node with available resources to spin a pod   
3. Binds the Pod to a given node   
   
View more [here](https://www.youtube.com/watch?v=rDCWxkvPlAw)   
   
## How are labels and selectors used?   
   
## What QoS classes are there?   
   
   
- Guaranteed   
- Burstable   
- BestEffort   
   
## Explain Labels. What are they and why would one use them?   
   
Kubernetes labels are key-value pairs that can connect identifying metadata with Kubernetes objects.   
   
## Explain Selectors   
   
## What is Kubeconfig?   
   
## What is Gatekeeper?   
   
[Gatekeeper docs](https://open-policy-agent.github.io/gatekeeper/website/docs): "Gatekeeper is a validating (mutating TBA) webhook that enforces CRD-based policies executed by Open Policy Agent"   
   
## Explain how Gatekeeper works   
   
On every request sent to the Kubernetes cluster, Gatekeeper sends the policies and the resources to OPA (Open Policy Agent) to check if it violates any policy. If it does, Gatekeeper will return the policy error message back. If it isn't violates any policy, the request will reach the cluster.   
   
## What is Conftest?   
   
Conftest allows you to write tests against structured files. You can think of it as tests library for Kubernetes resources.<br>   
It is mostly used in testing environments such as CI pipelines or local hooks.   
   
## What is Datree? How is it different from Conftest?   
   
Same as Conftest, it is used for policy testing and enforcement. The difference is that it comes with built-in policies.   
   
## What is Helm?   
   
Package manager for Kubernetes. Basically the ability to package YAML files and distribute them to other users and apply them in the cluster(s).   
   
## Why do we need Helm? What would be the use case for using it?   
   
Sometimes when you would like to deploy a certain application to your cluster, you need to create multiple YAML files/components like: Secret, Service, ConfigMap, etc. This can be tedious task. So it would make sense to ease the process by introducing something that will allow us to share these bundle of YAMLs every time we would like to add an application to our cluster. This something is called Helm.   
   
A common scenario is having multiple Kubernetes clusters (prod, dev, staging). Instead of individually applying different YAMLs in each cluster, it makes more sense to create one Chart and install it in every cluster.   
   
Another scenario is, you would like to share what you've created with the community. For people and companies to easily deploy your application in their cluster.   
   
## Explain "Helm Charts"   
   
Helm Charts is a bundle of YAML files. A bundle that you can consume from repositories or create your own and publish it to the repositories.   
   
## It is said that Helm is also Templating Engine. What does it mean?   
   
It is useful for scenarios where you have multiple applications and all are similar, so there are minor differences in their configuration files and most values are the same. With Helm you can define a common blueprint for all of them and the values that are not fixed and change can be placeholders. This is called a template file and it looks similar to the following   
   
```
apiVersion: v1
kind: Pod
metadata:
  name: {[ .Values.name ]}
spec:
  containers:
  - name: {{ .Values.container.name }}
  image: {{ .Values.container.image }}
  port: {{ .Values.container.port }}
```
   
   
The values themselves will in separate file:   
   
```
name: some-app
container:
  name: some-app-container
  image: some-app-image
  port: 1991
```
   
   
## What are some use cases for using Helm template file?   
   
   
- Deploy the same application across multiple different environments   
- CI/CD   
   
## Explain the Helm Chart Directory Structure   
   
someChart/ -> the name of the chart   
Chart.yaml -> meta information on the chart   
values.yaml -> values for template files   
charts/ -> chart dependencies   
templates/ -> templates files :)   
   
## How do you search for charts?   
   
`helm search hub [some_keyword]`   
   
## Is it possible to override values in values.yaml file when installing a chart?   
   
Yes. You can pass another values file:   
`helm install --values=override-values.yaml [CHART_NAME]`   
   
Or directly on the command line: `helm install --set some_key=some_value`   
   
## How Helm supports release management?   
   
Helm allows you to upgrade, remove and rollback to previous versions of charts. In version 2 of Helm it was with what is known as "Tiller". In version 3, it was removed due to security concerns.   
   
## What security best practices do you follow in regards to the Kubernetes cluster?   
   
   
- Secure inter-service communication (one way is to use Istio to provide mutual TLS)   
- Isolate different resources into separate namespaces based on some logical groups   
- Use supported container runtime (if you use Docker then drop it because it's deprecated. You might want to CRI-O as an engine and podman for CLI)   
- Test properly changes to the cluster (e.g. consider using Datree to prevent kubernetes misconfigurations)   
- Limit who can do what (by using for example OPA gatekeeper) in the cluster   
- Use NetworkPolicy to apply network security   
- Consider using tools (e.g. Falco) for monitoring threats   
   
## Running <code>kubectl get pods</code> you see Pods in "Pending" status. What would you do?   
   
One possible path is to run `kubectl describe pod <pod name>` to get more details.<br>   
You might see one of the following:   
   
   
- Cluster is full. In this case, extend the cluster.   
- ResourcesQuota limits are met. In this case you might want to modify them   
- Check if PersistentVolumeClaim mount is pending   
   
If none of the above helped, run the command (`get pods`) with `-o wide` to see if the node is assigned to a node. If not, there might be an issue with scheduler.   
   
## Users unable to reach an application running on a Pod on Kubernetes. What might be the issue and how to check?   
   
One possible path is to start with checking the Pod status.   
   
1. Is the Pod pending? if yes, check for the reason with `kubectl describe pod <pod name>`   
   TODO: finish this...   
   
## What is Istio? What is it used for?   
   
Istio is an open source service mesh that helps organizations run distributed, microservices-based apps anywhere. Istio enables organizations to secure, connect, and monitor microservices, so they can modernize their enterprise apps more swiftly and securely.   
   
## What is the control loop? How it works?   
   
Explained [here](https://www.youtube.com/watch?v=i9V4oCa5f9I)   
   
## What are all the phases/steps of a control loop?   
   
   
- Observe - identify the cluster current state   
- Diff - Identify whether a diff exists between current state and desired state   
- Act - Bring current cluster state to the desired state (basically reach a state where there is no diff)   
   
## An engineer form your organization told you he is interested only in seeing his team resources in Kubernetes. Instead, in reality, he sees resources of the whole organization, from multiple different teams. What Kubernetes concept can you use in order to deal with it?   
   
Namespaces. See the following [namespaces question and answer](#namespaces-use-cases) for more information.