---
created: 1662133053814
desc: ''
id: 6ouqierqo1uvar1tj5xrpg5
title: Prometheus Monitoring in K8s
updated: 1662237931633
---
   
Related::  [kubernetes.helm](../devlog/kubernetes.helm.md), [kubernetes.K8s Operator](../devlog/kubernetes.K8s%20Operator.md)   
   
   
---   
   
**How to deploy the different moving parts of Prometheus to a K8s cluster?**   
   
There are different ways of achieving this:   
   
1. Create all config files for each Prometheus component yourself and execute them in the right order.   
2. Using a Operator(a manager for all Prometheus components).   
3. Using Helm Chart for Prometheus.   
   
We'll go with the 3rd option but make use of Operator for managing it once initialized with Helm.   
   
## Setup Helm Chart   
   
Add repo   
   
`helm repo add prometheus-community https://prometheus-community.github.io/helm-charts`   
   
`helm repo add stable https://kubernetes-charts.storage.googleapis.com/`   
   
`helm search repo prometheus-community`   
   
`helm install prometheus prometheus-community/kube-prometheus-stack`   
   
`kubectl get all` to verify   
   
`-oper` = managed by operator   
   
2 statefulSets will be created   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662235281/wiki/zj4ig2c9niuscbmndkbn.png)   
   
3 Deployments will be created   
   
and 3 ReplicaSets will be created as an underlying components of Deployments   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662235320/wiki/kkbx0mm5u6bc3skpflyv.png)   
   
You get K8s monitoring out-of-the-box with this setup.   
   
**1 DaemonSet**   
   
   
- Node Exporter DaemonSet that runs on every Worker Node.   
- Node Exporter component basically connects to the Server and translates the Worker Node metrics to Prometheus metrics for scraping.   
   
With this, we’ve setup:   
   
   
- Monitoring Stack   
- Configuration of K8s cluster for monitoring.   
  - Worker Nodes and other K8s components are monitored.   
   
`kubectl get configmap` to check all the ConfigMaps that were created for “configuring” this entire setup. They’re managed by Operator. It informs how to connect to default metrics (scraping). It also has the default rules file for Prometheus.   
   
`kubectl get secret` to get all the secrets that were created for Prometheus, Grafana, Operator. It includes certificates, username & passwords.   
   
`kubectl get crd` to get the Custom Resource Definitions that were created.   
   
**Additional Info:**   
   
`kubectl get statefulset` like what containers are running and what images they're based on etc.   
   
`kubectl describe statefulset <statefulset-name> > name.yaml` exporting it to file for syntax highlighting and indentation.   
   
`kubectl describe deployment <prometheus-name> > name.yaml`   
   
`kubectl get secret <secret-name> -o yaml > secret.yaml`   
   
`kubectl get configmap <rulesfile> -o yaml > rules.yaml`   
   
The operator orchestrates the monitoring stack.   
   
**To add/adjust alert rules?**   
**To adjust Prometheus configuration**   
   
## Access Grafana   
   
`kubectl get service`   
   
The Grafana service is of ClusterIP type which is internal only. They're not open to external requests. In prod, you'd usually configure Ingress and point Ingress rules to `prometheus-grafana`.   
   
In our setup, we'll use port-forwarding to access Grafana.   
   
`kubectl get deployment`   
   
`kubectl get pod`   
   
`kubectl logs <grafana-pod> -c grafana` to check the port on which Grafana is running(listening). The default user is `admin`   
   
`kubectl port-forward deployment/prometheus-grafana 3000` will open port 3000.   
   
To go `localhost:3000` for the login page.   
   
## To access Prometheus UI   
   
`kubectl port-forward <pod-name-oper> 9090`