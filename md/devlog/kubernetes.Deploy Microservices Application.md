---
created: 1662323924932
desc: ''
id: f3vzxx0mzicwo0dfqwj3aqd
title: Deploy Microservices Application
updated: 1662342480700
---
   
**Overview**   
   
   
- Deploy MS application to a K8s cluster.   
- It is an online shopping app, [source code](https://github.com/GoogleCloudPlatform/microservices-demo).   
   
**Key information**   
   
   
- You don't exactly need to understand how the application code works.   
- What MS we're going to deploy?   
- How do these MS connect to each other?   
- If they need any 3rd party services or DBs.   
- Which service is accessible from outside the cluster?   
  - What is the entrypoint service that gets the requests from the browser.   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1662324430/wiki/nzwn1ozy9axdcqd0dxvr.png)   
  - You sort of need to visualize which service is talking to which other service.   
- Image names for each MS.   
- Environment variables for each MS.   
- Depending on how many teams are working on developing the MS, we'll create that many namespaces. If theres only one team responsible for all the MSes you'll only create one NS.   
   
You can find the finished code at [k8s-config · zubayrrr / online-shop-microservices-deployment](https://gitlab.com/zubayrrr/online-shop-microservices-deployment/-/tree/master/k8s-config)   
   
**Create Deployment & Service**   
   
For each MS.   
   
`mkdir online-shop-microservices`   
`touch config.yaml`   
   
Open the file in your preferred code editor.   
   
Both Deployment and Service for all the 11 Microservices will go inside one file or you can split them up.   
   
```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: emailservice
spec:
  selector:
    matchLabels:
      app: emailservice
  template:
    metadata:
      labels:
        app: emailservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/emailservice
          ports:
            - containerPort: 8080
          env:
            - name: PORT
              value: "8080"
---
apiVersion: v1
kind: Service
metadata:
  name: emailservice
spec:
  type: ClusterIP
  selector:
    app: emailservice
  ports:
    - protocol: TCP
      port: 5000
      targetPort: 8080

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: recommendationservice
spec:
  selector:
    matchLabels:
      app: recommendationservice
  template:
    metadata:
      labels:
        app: recommendationservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/recommendationservice
          ports:
            - containerPort: 8080
          env:
            - name: PORT
              value: "8080"
            - name: PRODUCT_CATALOG_SERVICE_ADDR
              value: "productcatalogservice:3550"
---
apiVersion: v1
kind: Service
metadata:
  name: recommendationservice
spec:
  type: ClusterIP
  selector:
    app: recommendationservice
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: paymentservice
spec:
  selector:
    matchLabels:
      app: paymentservice
  template:
    metadata:
      labels:
        app: paymentservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/paymentservice
          ports:
            - containerPort: 50051
          env:
            - name: PORT
              value: "50051"
---
apiVersion: v1
kind: Service
metadata:
  name: paymentservice
spec:
  type: ClusterIP
  selector:
    app: paymentservice
  ports:
    - protocol: TCP
      port: 50051
      targetPort: 50051

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: productcatalogservice
spec:
  selector:
    matchLabels:
      app: productcatalogservice
  template:
    metadata:
      labels:
        app: productcatalogservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/productcatalogservice
          ports:
            - containerPort: 3550
          env:
            - name: PORT
              value: "3550"
---
apiVersion: v1
kind: Service
metadata:
  name: productcatalogservice
spec:
  type: ClusterIP
  selector:
    app: productcatalogservice
  ports:
    - protocol: TCP
      port: 3550
      targetPort: 3550

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: currencyservice
spec:
  selector:
    matchLabels:
      app: currencyservice
  template:
    metadata:
      labels:
        app: currencyservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/currencyservice
          ports:
            - containerPort: 7000
          env:
            - name: PORT
              value: "7000"
---
apiVersion: v1
kind: Service
metadata:
  name: currencyservice
spec:
  type: ClusterIP
  selector:
    app: currencyservice
  ports:
    - protocol: TCP
      port: 7000
      targetPort: 7000

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: shippingservice
spec:
  selector:
    matchLabels:
      app: shippingservice
  template:
    metadata:
      labels:
        app: shippingservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/shippingservice
          ports:
            - containerPort: 50051
          env:
            - name: PORT
              value: "50051"
---
apiVersion: v1
kind: Service
metadata:
  name: shippingservice
spec:
  type: ClusterIP
  selector:
    app: shippingservice
  ports:
    - protocol: TCP
      port: 50051
      targetPort: 50051

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: adservice
spec:
  selector:
    matchLabels:
      app: adservice
  template:
    metadata:
      labels:
        app: adservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/adservice
          ports:
            - containerPort: 9555
          env:
            - name: PORT
              value: "9555"
---
apiVersion: v1
kind: Service
metadata:
  name: adservice
spec:
  type: ClusterIP
  selector:
    app: adservice
  ports:
    - protocol: TCP
      port: 9555
      targetPort: 9555

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cartservice
spec:
  selector:
    matchLabels:
      app: cartservice
  template:
    metadata:
      labels:
        app: cartservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/cartservice
          ports:
            - containerPort: 7070
          env:
            - name: REDIS_ADDR
              value: "redis-cart:6379"
---
apiVersion: v1
kind: Service
metadata:
  name: cartservice
spec:
  type: ClusterIP
  selector:
    app: cartservice
  ports:
    - protocol: TCP
      port: 7070
      targetPort: 7070

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: checkoutservice
spec:
  selector:
    matchLabels:
      app: checkoutservice
  template:
    metadata:
      labels:
        app: checkoutservice
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/checkoutservice
          ports:
            - containerPort: 5050
          env:
            - name: PORT
              value: "5050"
            - name: PRODUCT_CATALOG_SERVICE_ADDR
              value: "productcatalogservice:3550"
            - name: SHIPPING_SERVICE_ADDR
              value: "shippingservice:50051"
            - name: PAYMENT_SERVICE_ADDR
              value: "paymentservice:50051"
            - name: EMAIL_SERVICE_ADDR
              value: "emailservice:5000"
            - name: CURRENCY_SERVICE_ADDR
              value: "currencyservice:7000"
            - name: CART_SERVICE_ADDR
              value: "cartservice:7070"
---
apiVersion: v1
kind: Service
metadata:
  name: checkoutservice
spec:
  type: ClusterIP
  selector:
    app: checkoutservice
  ports:
    - protocol: TCP
      port: 5050
      targetPort: 5050

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
spec:
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
        - name: server
          image: gcr.io/google-samples/microservices-demo/frontend
          ports:
            - containerPort: 8080
          env:
            - name: PORT
              value: "8080"
            - name: PRODUCT_CATALOG_SERVICE_ADDR
              value: "productcatalogservice:3550"
            - name: CURRENCY_SERVICE_ADDR
              value: "currencyservice:7000"
            - name: CART_SERVICE_ADDR
              value: "cartservice:7070"
            - name: RECOMMENDATION_SERVICE_ADDR
              value: "recommendationservice:8080"
            - name: SHIPPING_SERVICE_ADDR
              value: "shippingservice:50051"
            - name: CHECKOUT_SERVICE_ADDR
              value: "checkoutservice:5050"
            - name: AD_SERVICE_ADDR
              value: "adservice:9555"
---
apiVersion: v1
kind: Service
metadata:
  name: frontend
spec:
  type: ClusterIP
  selector:
    app: frontend
  ports:
    - name: http
      port: 80
      targetPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: frontend-external
spec:
  type: NodePort
  selector:
    app: frontend
  ports:
    - name: http
      port: 80
      targetPort: 8080
      nodePort: 30007

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-cart
spec:
  selector:
    matchLabels:
      app: redis-cart
  template:
    metadata:
      labels:
        app: redis-cart
    spec:
      containers:
        - name: redis
          image: redis:alpine
          ports:
            - containerPort: 6379
          volumeMounts:
            - mountPath: /data
              name: redis-data
      volumes:
        - name: redis-data
          emptyDir: {}
---
apiVersion: v1
kind: Service
metadata:
  name: redis-cart
spec:
  type: ClusterIP
  selector:
    app: redis-cart
  ports:
    - name: redis
      port: 6379
      targetPort: 6379
```
   
   
## Spin up a LKE cluster   
   
Download `kubeconfig.yaml` and set permissions on it.   
   
`chmod 600 path/to/kubeconfig.yaml`   
   
OR   
   
`chmod 400 path/to/kubeconfig.yaml`   
   
AND   
   
`export KUBECONFIG=/path/to/kubeconfig.yaml`   
   
`kubectl get pod`   
   
Create a new namespace instead of deploying them into the default namespace.   
   
`kubectl create ns microservices`   
   
Deploy Microservices   
   
`kubectl apply -f config.yaml -n microservices`   
   
`kubectl get pod -n microservices`   
   
`kubectl get svc -n microservices`   
   
   
---   
   
# Production & Security Best Practices   
   
## Pinned (Tag) Version   
   
For each container Image.   
   
Specify a pinned version on each container image. When you don't specify a version tag, K8s will pull the latest version of that image which can be a security issue as it might have bugs, it can break things, act unpredictably. Fixating on a version gives a clearer picture of what versions of Images are running on the cluster.   
   
## Liveness Probe   
   
For each container.   
   
There may come cases where the Pod stays running but the application inside it might die. To let K8s know about the status of the container/application inside the Pod so K8s automatically restarts the Pod whenever something goes awry.   
   
K8s can perform health checks using Liveness Probe. It is a simple script/program that pings the application every now and then to check if its running. You can write such a program yourself or Devs might provide it for you.   
   
`livenessProbe` is a container attribute. It takes two parameter, how often/regularly the endpoint of the application should be checked.   
   
**While application is running**   
   
```yaml
containers:
  livenessProbe:
    periodSeconds: 5
    exec:
      command: ["/bin/grpc_health_probe", "-addr=:8080"] # this program is coming from the container Image itself.
```
   
   
**TCP Probe**   
   
```yaml
containers:
  livenessProbe:
    periodSeconds: 5
    tcpSocket:
      port: <application-port>
```
   
   
## Readiness Probe   
   
For each container.   
   
Liveness probe only helps K8s check that the application is running successfully ONLY after the container/application starts.   
   
**During application startup**   
   
**What about the startup process itself?**   
   
Readiness Probe lets K8s know if the application is ready to receive traffic. Without it, K8s assumes tha the app is ready to receive traffic while your application is starting up and you'll be left with a bunch of errors/warnings in your logs.   
   
```yaml
containers:
  readinessProbe:
    periodSeconds: 5
    exec:
      command: ["/bin/grpc_health_probe", "-addr=:8080"]
```
   
   
when you do `kubectl get pod` you can check "READY" for `1/1` if its really ready or `0/1` if it is'nt.   
   
**TCP Probes**   
   
`kubelet` makes probe connection at the node not in the pod.   
   
`kubelet` will attempt to open a socket on your container on the specific application port, if it succeeds in establishing a connection the container is considered to be healthy/ready/reachable.   
   
```yaml
containers:
  readinessProbe:
    periodSeconds: 5
    tcpSocket:
      port: <application-port>
```
   
   
**initialDelaySeconds**   
   
```yaml
containers:
  readinessProbe:
    initialDelaySeconds: 5 # tells kubelet to wait 5 seconds before performing liveness/readiness probe
    periodSeconds: 5
    tcpSocket:
      port: <application-port>
```
   
   
**HTTP Probes**   
   
`kubelet` sends an HTTP request to specified path and port.   
   
```yaml
containers:
  livenessProbe:
    periodSeconds: 5
    httpGet:
      path: /url/of/health-endpoint
      port: <application-port>
```
   
   
## Resource Requests   
   
For each container.   
   
Configure resource requests for each container.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662333124/wiki/q9qcsxpndp1d2oou88a0.png)   
   
Some applications may need more CPU and Memory resource than others, to make sure that your application/container gets enough resources when it starts inside a Pod, you should define resource request for each of your container.   
   
Requests is what the container is guaranteed to get.   
   
K8s scheduler uses this to figure out where to run the Pods.   
   
**Keep CPU request at “1” or below**   
   
CPU resources are defined in millicores.   
Memory resources are defined in mebibyte.   
   
```yaml
containers:
	requests:
		cpu: 100m
		memory: 64mi
```
   
   
## Resource Limits   
   
What if your container/application starts consuming more than it requested? If not limited, that container can consume all the Node’s resources other Pods running on the same Node will not have enough resources.   
   
To make sure:   
   
   
- Container never goes above a certain value.   
- Container is only allowed to go up to the limit and not beyond.   
   
```yaml
containers:
	requests:
		cpu: 100m
		memory: 64Mi
	limits:
		cpu: 200m
		memory: 128Mi
```
   
   
Some Microservices may require more resources than others. In which case, you can check with the Devs and fix the values for those services respectively.   
   
## DON’T expose a NodePort   
   
When exposing a service of `NodePort` service type, it can be a security risk as it opens a `nodePort` on all Worker Nodes in the cluster that can be directly accessed by external sources. The attack surface increases as there are multiple entrypoints in the cluster.   
   
Ideally:   
   
   
- You should only use Internal Service(ClusterIP).   
- Your cluster should only have 1 entrypoint.   
- The entrypoint should be outside the cluster on a separate server.   
   
Instead of using `NodePort` service type, you can use `LoadBalancer` which uses the cloud provider’s native LoadBalancer to create an external entrypoint into the cluster.   
   
OR   
   
You can use an Ingress Controller to direct traffic to the internal services.   
   
## More than 1 Replica   
   
For Deployment   
   
The number of replicas when undefined is 1 but you should always have more than 1 Replicas for your Deployments.   
   
If your 1 Pod crashes, your application will not be accessible until a new Pod starts(restarts). Creating a downtime.   
   
## More than 1 Worker Node   
   
Always use more than 1 Worker Node for your cluster. You've a single point of failure with just 1 Node. You should also replicate your Nodes. Your replicas should run on different Node otherwise having replicas becomes pointless.   
   
## Use Labels   
   
Use Labels for all your resources. Labeling your K8s components is like giving custom identifiers.   
   
Labels are key-value pairs that are attached to resources/components. They should be meaningful and relevant to users so you can reference them in other resources.   
   
Use cases involve grouping Pods based on the labels they share and referencing them using `selector` attribute it in Service component.   
   
## Use Namespaces   
   
USe Namespaces to isolate resources. Logically grouping applications and other components in Namespaces makes managing the cluster easier. It can also be used for **Access Rights based on Namespaces** like diving up your dev teams. You can have 1 Namespace per Microservice as well.   
   
## 3 Security Best Practices   
   
1. Ensure Images are free of vulnerabilities.   
   
   
- That goes for third-party libraries/dependencies.   
- Employ Manual Vulnerability Scans or Automated Scans in Build Pipeline.   
   
2. No Root Access for containers.   
   
   - Configure containers to use unprivileged users.   
   - Most official Images do not use root user that isn't the same for unofficial Images.   
3. Update Kubernetes to latest version.   
   
   - Update it Node by Node to avoid cluster downtime.