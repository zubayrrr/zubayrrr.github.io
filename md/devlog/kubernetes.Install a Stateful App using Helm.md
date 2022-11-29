---
created: 1662082070213
desc: ''
id: p3brq3akdajllutvq926pi3
title: Install a Stateful App using Helm
updated: 1662082070213
---
   
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