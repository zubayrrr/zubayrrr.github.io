---
created: 1661869499550
desc: ''
id: i76fk21qoqacqdkxt09q5fg
title: Prometheus Stack in Kubernetes
updated: 1662770208804
---
   
Related::  [kubernetes.helm](../devlog/kubernetes.helm.md), [kubernetes.K8s Operator](../devlog/kubernetes.K8s%20Operator.md)   
   
   
---   
   
Different components of a Prometheus stack:   
   
   
- Statefulset   
- AlertManager   
- Grafana   
- Deployments   
- ConfigMaps   
- Secrets   
   
There are several different ways of deploying different parts of Prometheus stack on [Kubernetes](../devlog/kubernetes.md) cluster.   
   
1. Creating all configuration files yourself for all the parts/components of your Prometheus Stack and execute them in the right order. This way requires a lot of effort and knowledge of what you're doing.   
2. Using an operator. Manager for all the individual components. It manages the combination of all the components as one unit.   
   1. Find Prometheus operator.   
   2. Deploy in a K8s cluster.   
3. Using Helm chart to deploy operator. Prometheus operator has a Helm chart that is maintained by Helm community.   
   
   - Helm will do the initial setup.   
   - Operator will manage the setup.   
   
We'll go with the 3rd option but make use of Operator for managing it once initialized with Helm.   
   
**Overview**   
   
   
- Deploy Microservices Application   
- Deploy Prometheus Stack   
- Monitor Kubernetes cluster   
- Monitor Microservices Application   
   
   
---   
   
## Create an [aws.EKS](../devlog/aws.EKS.md) cluster   
   
using `eksctl`   
   
1. `eksctl create cluster`   
2. `kubectl get node` to get nodes   
3. `kubectl apply -f config-microservices.yaml` to deploy [Deploy Microservices Application](/not_created.md) on the cluster.   
   
## Deploy Prometheus stack using [Helm](../devlog/helm.md)   
   
1. `helm repo add prometheus-community https://prometheus-community.github.io/helm-charts` to add helm chart repo.   
2. `helm repo update`   
   
**Install Prometheus into own namespace.**   
   
3. `kubectl create namespace monitoring`   
4. `helm install monitoring prometheus-community/kube-prometheus-stack -n monitoring` installing helm chart   
5. Check if Prometheus pods are running `kubectl --namespace monitoring get pods -l "release=monitoring"` or `kubectl get all -n monitoring`   
   
`-oper` = managed by operator   
   
## Understanding Prometheus Stack   
   
**2 StatefulSets**   
   
Prometheus Pod is managed by Operator.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662235281/wiki/zj4ig2c9niuscbmndkbn.png)   
   
   
- Prometheus Server.   
- AlertManager.   
   
**3 Deployments**   
   
   
- Prometheus Operator.   
  - Created Prometheus and AlertManager StatefulSet.   
- Grafana.   
- Kube State Metrics.   
  - This is a Helm Chart itself but is a dependency of the Prometheus Helm Chart.   
  - Scrapes K8s components, it monitors the health of the entire stack inside the cluster and makes it available to Prometheus for scraping.   
   
With this setup, you get K8s monitoring out-of-the-box.   
   
**3 ReplicaSet**   
   
These are created as underlying components of Deployments   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662235320/wiki/kkbx0mm5u6bc3skpflyv.png)   
   
**1 DaemonSet**   
   
   
- Node Exporter DaemonSet.   
- DaemonSet runs on every single Worker Node.   
- Node Exporter connect to the server and translates the server metrics(Worker Nodes) and transforms them into Prometheus metrics.   
   
With this, we’ve setup:   
   
   
- Monitoring Stack   
- Configuration of K8s cluster for monitoring.   
  - Worker Nodes and other K8s components are monitored.   
   
`kubectl get configmap` to check all the ConfigMaps that were created for “configuring” this entire setup. They’re managed by Operator. It informs how to connect to default metrics (scraping). It also has the default rules file for Prometheus.   
   
`kubectl get secret` to get all the secrets that were created for Prometheus, Grafana, Operator. It includes certificates, username & passwords.   
   
`kubectl get crd` to get the Custom Resource Definitions that were created.   
   
**Additional Info:**   
   
`kubectl get statefulset -n monitoring` like what containers are running and what images they're based on etc.   
   
`kubectl describe statefulset <statefulset-name> > name.yaml` exporting it to file for syntax highlighting and indentation.   
   
`kubectl describe deployment <prometheus-name> > name.yaml`   
   
`kubectl get secret <secret-name> -o yaml > secret.yaml`   
   
`kubectl get configmap <rulesfile> -o yaml > rules.yaml`   
   
The operator orchestrates the monitoring stack.   
   
**To add/adjust alert rules?**   
**To adjust Prometheus configuration**   
   
## Access Prometheus UI   
   
`kubectl port-forward service/monitoring-kube-prometheus-prometheus -n monitoring 9090:9090 &` to run Prometheus UI in background   
   
We can find information like:   
   
   
- What targets is Prometheus monitoring?   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662768947/wiki/manks4t1kghxt8rdv51m.png)   
   
Prometheus jobs - for metrics   
Job label - instance label   
   
Prometheus UI is not ideal for data visualization - its useful for debugging, filtering metrics, checking targets, jobs and the entire Prometheus configuration.   
   
## Access Grafana   
   
It has access to all the metrics Prometheus scraped. It is ideal for visualising metrics overtime.   
   
`kubectl port-forward service/monitoring-grafana 8080:80 -n monitoring`   
   
`127.0.0.1:8080/login`