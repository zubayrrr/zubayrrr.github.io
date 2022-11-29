---
created: 1661962002447
desc: ''
id: 4p4lussvh2izprt2vpsfkd8
title: ConfigMap and Secret
updated: 1661962002447
---
   
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