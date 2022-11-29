---
created: 1661954297479
desc: ''
id: qn4402aho657asdik4k4gh7
title: Deploying mongoDB and mongo-express in Kubernetes Cluster
updated: 1661954297479
---
   
**Overview**   
   
   
- We'll create a MongoDB Pod and in order to talk to that pod, we'll need a [kubernetes.services](../devlog/kubernetes.services.md), specifically an internal service(no external requests are allowed, only components in the same cluster can talk to it).   
- We'll create mongo-express deployment.   
  - we'll need DB Url of MongoDB so mongo-express can connect to it. ([kubernetes.ConfigMap and Secret](../devlog/kubernetes.ConfigMap%20and%20Secret.md))   
  - DB User and DB PW for authentication. ([kubernetes.ConfigMap and Secret](../devlog/kubernetes.ConfigMap%20and%20Secret.md))   
  - We'll pass these values as env variables in deployment configuration file. Both ConfigMap and Secrets will be referenced for values.   
- Create an external service to make mongo-express available from the web and talk to the pod.   
   
The flow looks like:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661954766/wiki/rnjrz6pxvo6ntyvyfkdn.png)   
   
## Start cluster via [Minikube](/not_created.md)   
   
`minikube start`   
   
`kubectl get all`   
   
## Create MongoDB deployment   
   
```yaml
# mongo.yml
apiVersion: apps/v1
kind: deployment
metadata:
  name: mongodb-deployment
  labels:
    app: mongodb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
        - name: mongodb
          image: mongo
          ports:
            - containerPort: 27017
          env:
            - name: MONGO_INITDB_ROOT_USERNAME
              valueFrom:
                secretKeyRef:
                  name: mongodb-secret
                  key: mongo-root-username
            - name: MONGO_INITDB_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mongodb-secret
                  key: mongo-root-password
```
   
   
`kubectl apply -f mongo.yml`   
`kubectl get all`   
`kubectl get pod --watch`   
   
## Create Secret   
   
For `MONGO_INITDB_ROOT_USERNAME` & `MONGO_INITDB_ROOT_PASSWORD`. **They should be created before the Deployment**(the order matters).   
   
```yaml
# mongo-secret.yml
apiVersion: v1
kind: Secret
metadata:
  name: mongodb-secret
type: Opaque # for arbitrary key-value pairs
data: # the values should be base64 encoded, encryption is not enabled by default.
  mongo-root-username:
  mongo-root-password:
```
   
   
To encode values in base64:   
   
`echo -n 'username' | base64`   
`echo -n 'password' | base64`   
   
To create the secrets using `mongo-secrets.yml`   
   
`kubectl apply -f mongo-secret.yml`   
`kubectl get secret`   
   
## Create internal service   
   
We can either create it in a separate file or use the multi document in one file - feature of yaml and define it inside the `mongo.yml` after `---`. Internal service is default. AKA ClusterIP.   
   
```yaml
___
apiVersion: 1
kind: Service
metadata:
  name: mongodb-service
spec:
  selector:
    app: mongodb
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
```
   
   
`kubectl apply -f mongo.yml` to create the service.   
`kubectl get service`   
`kubectl describe service mongodb-service` to confirm if it's connected to the correct pod.   
   
   
---   
   
**Deployment for mongo-express**   
   
```yaml
# mongo-express.yaml
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
                valueFrom:
                  secretKeyRef:
                    name: mongodb-secret
                    key: mongo-root-username
              - name: ME_CONFIG_MONGODB_ADMINPASSWORD
                valueFrom:
                  secretKeyRef:
                    name: mongodb-secret
                    key: mongo-root-password
              - name: ME_CONFIG_MONGODB_SERVER
                valueFrom:
                  configMapKeyRef:
                    name: mongodb-configmap
                    key: database_url
```
   
   
`kubectl apply -f mongo-express.yml`   
`kubectl get pod`   
   
## Create ConfigMap   
   
**ConfigMap must already exist in the K8s cluster when referencing it.**   
   
```yaml
mongo-configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mongodb-configmap
data:
  database_url: mongodb-service
```
   
   
`kubectl apply -f mongo-configmap.yaml`   
   
## Create external service   
   
To make a service an external service you add a `type: LoadBalancer` and `nodePort: 30000` (port for external IP, the port you put into browser), even though internal service also acts as a LoadBalancer. It assigns service an external IP address to accept external requests.   
   
```yaml
---
apiVersion: v1
kind: Service
metadata:
  name: mongo-express-service
spec:
  selector:
    app: mongo-express
  type: LoadBalancer
  ports:
    - protocols: TCP
      port: 8081
      targetPort: 8081
      nodePort: 30000
```
   
   
`kubectl apply -f mongo-express.yaml`   
`kubectl get service`   
   
`minikube service mongo-express-service` will assign external service a public IP address on clusters running on minikube.