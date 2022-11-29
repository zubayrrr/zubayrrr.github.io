---
created: 1662124906924
desc: ''
id: 2qtiwotfbxan87tzfrg4e9u
title: Deploying Images from private Docker repository
updated: 1662124906924
---
   
Deploy your application in a Kubernetes cluster from a private repository.   
   
A common workflow when building your own images and storing them on private repositories looks like this:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662125047/wiki/cqpwo6w7zd1igdtkipla.png)   
   
The question now remains is, how do you get those images from the private repositories into your Kubernetes cluster?   
   
   
**Steps to pull images from private repository**   
   
1. Create Secret component.   
   
	- That contains access token or credentials to your Docker registry.   
2.  Configure Deployment/Pod to use the Secret using `imagePullSecrets` attribute.   
   
For this demo we’ll go with [aws.ECR](../devlog/aws.ecr.md) and we’ll use a simple Nodejs application.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662125406/wiki/aqee8js7evzep6kmfcp4.png)   
   
   
## Docker Login   
   
create `config.json` file for Secret.   
   
`aws ecr get-login` will throw the entire `docker login` command that will get executed for logging you in.   
   
It’ll create a `.docker/config.json` that holds the authentication information. The access token will either be stored in your config file or via an external credentials manager(like of your operating system).   
   
With [kubernetes.Minikube](../devlog/kubernetes.Minikube.md). It won’t be able to use `credStore` to fetch the token as it runs virtually.   
   
You can `docker login` directly inside `minikube`.   
   
`minikube ssh`   
   
Copy paste the command `aws ecr get-login` generated inside `minikube`.   
   
## Create Secret   
   
   
```yaml
apiVersion: v1
kind: Secret 
metadata: 
	name: my-registry-key
data:
	.dockerconfigjson: # base 64 encoded contents of .docker/config.json
type: kubernetes.io/dockerconfigjson 
```
   
   
To create secret and set it as values for the attributes. Use this method if you don’t wanna manually encode the values and paste them inside `secret-config.yaml` and then apply the changes.   
   
```bash
kubectl create secret generic my-registry-key \
--from-file=.dockerconfigjson=.docker/config.json \
--type=kubernetes.io/dockerconfigjson 
```
   
   
There’s another of setting up `docker login` and creating a secret in just one step:   
   
```
kubectl create secret docker-registry my-registry-key-two \
--docker-server=https://<docker-regsistry>.com \
--docker-username=AWS \ 
--docker-password=<password aws ecr get-login generated>
```
   
   
## Create Deployment    
   
```yaml
apiVersion: apps/v1
kind: Deployment 
metadata:
	name: my-app
	labels:
		app: my-app
spec:
	replicas: 1
	selector:
		matchLabels:
			app: my-app
	template:
		metadata:
			labels:
				app: my-app
		spec:
			imagePullSecrets:
			- name: my-registry-key
			containers:
			- name: my-app
				image: <image uri> # repository/image-name:version
				imagePullPolicy: Always
				ports:
					- containerPort: 3000
```
   
   
`kubectl apply -f path/to/my-app-deployment.yaml`   
   
> Note: Secret has to be in same namespace as Deployment