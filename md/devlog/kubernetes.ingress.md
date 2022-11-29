---
created: 1661974250244
desc: Connecting to Applications outside cluster
id: 5svmlpy5xnj1n5pgzirz6rs
title: Ingress
updated: 1661974250244
---
   
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