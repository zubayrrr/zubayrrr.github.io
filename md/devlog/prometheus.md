---
created: 1653569037304
desc: ''
id: 9fa6uf6xbnv00fv944o1y1o
title: Prometheus
updated: 1662779263648
---
   
Prometheus is a monitoring tool. It collects metrics and stores it with which we can make dashboards and alerts.   
   
It was created to monitor highly dynamic container environments like [kubernetes](../devlog/kubernetes.md), [docker swarm](../devlog/docker%20swarm.md) etc. It can also be used in traditional non-container infrastructure.   
   
Typically you've many servers that run containerized applications, hundreds of different processes running on that infrastructure which are all interconnected. To get insights on this infrastructure such as errors, latency etc.   
   
To make it easier for us to debug these system and fix them without much downtime, we'll use something like Prometheus, that will constantly monitor all the services/resources, alerts the maintainers as soon as anything goes wrong. **In fact it can identify problems before they even occur** and notify the maintainers so the failures can be prevented.   
   
# Prometheus Architecture   
   
## Prometheus Server   
   
This is what does the actual monitoring.   
   
It constitutes of three components:   
   
   
- Time Series DB - stores metrics data, no. of exceptions.   
- Data Retrieval Worker - responsible for pulling metrics from applications/services/servers - target resources and pushing them to the Time series DB.   
- HTTP Server - Accepts PromQL queries for that stored data. Web server API is used to display data in a dashboard or UI - either Prometheus UI or Grafana etc.   
   
## Targets and Metrics   
   
What does Prometheus monitor?   
   
It can be an entire [linux](../topics/linux.md) server, Windows server, a standalone [apache](../devlog/apache.md) server, single application or service. These are called as **Targets**.   
   
Each target has unit of monitoring:   
   
   
- For a Linux server it could be current CPU usage, memory usage, disk space usage.   
- For an application - No. of exceptions, requests, request duration.   
   
A unit that you'd want to monitor for a target is called a **Metric**.   
They're what gets stored in Prometheus DB component. Prometheus defines human readable, text based format for the metrics. Metric entries or data has `TYPE` and `HELP` attributes to increase it's readability.   
   
`HELP` is basically description of the metric.   
`TYPE` is one of three metric types:   
   
   
- `Counter`   
  - For how many times x happened   
- `Gauge`   
  - For a metric that can go up and down. Eg: Current value of x now?   
- `Histogram`   
  - For tracking how long something took or how big something was(like the size of a request).   
   
## Getting metrics   
   
How does Prometheus collect metrics from the targets?   
   
**Pulling**   
   
Your application(regardless of technology) will have to expose a metrics HTTP endpoint and Prometheus will scrape from the endpoint. By default is is: `hostaddress/metrics`.   
   
Data available in the `/metrics` endpoint should be in the correct format that Prometheus understands.   
   
Some servers expose Prometheus endpoints by default so you don't really have to do extra work for it. But many services don't have native Prometheus endpoints in which case you'd need an **Exporter**   
   
**Exporter**   
   
It is basically a script/service that fetches metrics from your target and converts them in format Prometheus understands and exposes it's converted data at it's own `/metrics` endpoint where Prometheus can scrape them.   
   
Prometheus has a list of exporters for different services like [MySQL](../devlog/mysql.md), [Elasticsearch](../devlog/Elasticsearch.md), [linux](../topics/linux.md) servers, [build automation](/not_created.md), Cloud Platforms and so on.   
   
If you want to monitor a Linux server, see: [Monitoring Linux host metrics with the Node Exporter | Prometheus](https://prometheus.io/docs/guides/node-exporter/)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656150261/wiki/xfe8c37gmzogdoin3wtx.png)   
   
Exporters are also available as Docker images. SO   
   
If you want to monitor [mysql](../devlog/mysql.md) container in a [kubernetes](../devlog/kubernetes.md) cluster, you can deploy a sidecar container of MySQL exporter that will run inside the pod with MySQL container, connect to it and start sending MySQL metrics for Prometheus and making them available at it’s own `/metrics` endpoint.   
   
**Monitoring your own applications?**   
   
   
- How many requests your applications are receiving.   
- How many exceptions are occurring.   
- How many server resources your application is using.   
   
For this you can use Client Libraries for different languages using which you can expose `/metrics` endpoint for metrics that are relevant to you.   
[Client libraries | Prometheus](https://prometheus.io/docs/instrumenting/clientlibs/)   
   
## Push based VS Pull based   
   
Most monitoring systems like [aws.CloudWatch](../devlog/aws.CloudWatch.md) or [New Relic](../devlog/new%20relic.md) etc use a Push system. Applications and servers are responsible for pushing their metric data to a centralized collection platform of that monitoring tool.   
   
In large microservices based system this approach can create a bottleneck for your infrastructure as all of these microservices constantly make push request to your monitoring tool thus flooding your system.   
   
Plus, you’ll also need to install additional software(daemons) on each of your targets to push the metrics to the monitoring server. In contrast with Prometheus which only requires a scraping endpoint.   
   
Multiple Prometheus instances can collect/pull metrics. Using pull, Prometheus can easily detect whether a service is up and running or not.   
   
Pushing can be ambiguous when checking if the service is up or not when compared to pull mechanism. Because there can be many reasons for a push request to fail.   
   
**Pushing**   
   
Pushgateway can be utilized when a target only runs for a short time.   
Eg: A batch job, scheduled job etc. For such jobs, Prometheus offers Pushgateway component. So these services can push metrics directly to Prometheus DB.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655885235/wiki/yguspabejdgcr4qbzegm.png)   
   
## Configuring Prometheus   
   
`prometheus.yaml` file contains all the info needed for Prometheus to know what(targets) to scrape and when(intervals).   
   
Prometheus then uses **Service Discovery** mechanism to find those target endpoints.   
   
You can find the sample config files with default values which comes with your first Prometheus installation.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656153062/wiki/p2l9ubydx8h1viv4pafn.png)   
   
Under `global:` you define how often Prometheus will scrape it’s targets.   
   
Rules are for aggregating metric values or creating alerts when conditions   
are met.   
   
`scrape_configs:` define what resources Prometheus monitors; essentially targets. You can define your own jobs and default values for each job(overwrite global interval values).   
   
Since Prometheus has it’s own `/metrics` endpoint, it can monitor it’s own health.   
   
## AlertManager   
   
How does Prometheus trigger alerts that are defined by rules in `prometheus.yaml` and who receives these alerts?   
   
Prometheus has a component called AlertManger that is responsible for firing alerts via different channels (Emails, Slack channel or other notification clients).   
   
Prometheus server will read alert rules and if the conditions under rules is met an alert is fired.   
   
## Prometheus Data Storage   
   
Where does Prometheus store all the data that it collects/aggregates? How can other systems use this data?   
   
Prometheus stores metric data on disks, includes Local on disk **Time Series DB** but also optionally integrates with remote storage system. It is stored in custom Time Series format. Because of this you cannot directly write this data on a relational DB or something else.   
   
Once collected, Prometheus lets you query the data through it’s server API using it’s query language called **PromQL**.   
   
## PromQL   
   
You can use Prometheus dashboard UI to ask Prometheus server via PromQL to for example show the status of a target right now.   
   
Or use more powerful data visualization tools like **Grafana** to display the data which uses PromQL under the hood to get data out of Prometheus .   
   
Example PromQL query to:   
   
Query all HTTP status codes except `4xx` ones   
   
```sql
http_requests_total{status!~"4.."}
```
   
   
This query does some subquery:   
   
Returns the 5 minute rate of the _http_requests_total_ metric for the past 30 minutes.   
   
```sql
rate(http_requests_total[5m]) [30m:]
```
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656153983/wiki/qu5c4x2hrwuozqeqebxy.png)   
   
## Salient Characteristics of Prometheus   
   
It is designed to be reliable even when other systems have an outage so you can diagnose the problems and fix them.   
   
Each Prometheus server is standalone and self-contained. It doesn’t depend on network storage or other remote services. It is meant to be still working when other parts of the infrastructure are broken.   
   
It doesn’t require extensive setup.   
   
**Drawbacks**:   
   
It can be difficult to scale, when you have hundreds of servers that you want to use multiple Prometheus instances for aggregation of metrics setting them up can get complicated.   
   
A workaround this would be to increase the capacity of your Prometheus server, limit the number of metrics Prometheus collects from applications.   
   
## Prometheus Federation   
   
To scale monitoring with scalable cloud apps.   
   
Prometheus Federation allows one Prometheus server to scrape data from another Prometheus server. This will allow you to scale your Prometheus setup with your multi-node applications.   
   
## Prometheus with [Docker](../devlog/docker.md) & [Kubernetes](../devlog/kubernetes.md)   
   
It is fully compatible with both.   
   
Prometheus components are available as Docker images and therefore can be deployed on Kubernetes or other container environments.   
   
It provides monitoring of K8s Cluster Node Resource out of the box! Once deployed on K8s, it starts gathering metrics data on each Kubernetes node server without any extra configuration.   
   
## [prometheus.grafana](../devlog/prometheus.grafana.md)   
   
## Alert Rules   
   
People don’t constantly keep a watch on dashboards for anomalies. Ideally when something wrong happens, you want to be notified so you can go check the dashboard.   
   
**Alerting** in Prometheus is separated into 2 parts.   
   
1. Define what we want to be notified about (Alert Rules)   
2. Trigger notification (AlertManager)   
   
Go to Prometheus UI > Alerts to find existing alert rules Prometheus stack created for us.   
   
Expand an alert to find the configuration of that alert rule.   
   
```yaml
groups:
  - name: example
    rules:
      - alert: HighRequestLatency
        expr: job:request_latency_seconds:mean5m{job="myjob"} > 0.5
        for: 10m
        labels:
          severity: page
        annotations:
          summary: High request latency
```
   
   
![https://res.cloudinary.com/zubayr/image/upload/v1662774449/wiki/fqyxvdsgnf7eootxptzk.png](https://res.cloudinary.com/zubayr/image/upload/v1662774449/wiki/fqyxvdsgnf7eootxptzk.png)   
   
The syntax/attributes are defined as:   
   
   
- name: descriptive name of the alert   
- expr: logical expression defined in PromQL   
  - [Query functions | Prometheus](https://prometheus.io/docs/prometheus/latest/querying/functions/)   
- for: causes Prometheus to wait for certain duration   
- annotations: specifies a set of informational labels for longer additional information.   
   
## Create Alert Rules   
   
1. Alert when CPU usage > 50%.   
2. Alert when Pod cannot start.   
   
```yaml
# 1st alert
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
	name: main-rules
	namespace: monitoring
	labels:
		app: kube-prometheus-stack
		release: monitoring 
spec:
	groups:  # grouping alert rules
	- name: main.rules
	- rules: 
		- alert: HostHighCpuLoad
			expr: 100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idel"}[2m])) * 100) > 50
			for: 10m
			labels:
				severity: warning
				namespace: monitoring
			annotations:
				description: "CPU load on host is over 50%\ Value = {{ $value }}\n Instance = {{ $labels.instance }}"
				summary: "Host CPU load high"
		- alert: kubernetesPodCrashLooping
			expr: kube_pod_container_status_restarts_total > 5
			for: 0m
			labels:
				severity: critical
				namespace: monitoring
			annotations:
				description: "Pod {{ $labels.pod }} is crash looping\n Value = {{ $value }}"
				summary: "Kubernetes Pod is crash looping"
```
   
   
**Adding the Alert Rule to K8s**   
   
Since we’re running Prometheus as an operator on K8s, we can run a custom K8s component defined by CRDs which basically informs K8s of the new alert rule that was added and add it to the list of alert rules.   
   
If the Prometheus stack wasn’t running as operator, we’d have to manually edit the rule file and reload Prometheus application.   
   
Operator takes our custom K8s resource and tells Prometheus to reload the alert rules.   
   
## Applying Alert Rules   
   
`kubectl apply -f alert-rules.yaml`   
   
`kubectl get PrometheusRule -n monitoring`   
   
Prometheus operator should now pick the new rules and ask Prometheus to restart with new alert rules.   
   
To make sure operator picked up the new rules you can check the logs.   
   
`kubectl get pod -n monitoring`   
   
`kubectl logs prometheus-monitoring-kube-prometheus-prometheus-0 -n monitoring -c config-reloader`   
   
We can also check the logs of Prometheus itself   
   
`kubectl logs prometheus-monitoring-kube-prometheus-prometheus-0 -n monitoring -c prometheus`   
   
To test the rules   
   
Get Docker Image “cpustress” to stimulate CPU stress and deploy it as a Pod on our cluster.   
   
`kubectl run cpu-test --image=containerstack/cpustress -- --cpu 4 --timeout 30s --metrics-brief`   
   
   
## Firing state    
   
Firing state basically means the alert is sent to AlertManager.   
   
Now the AlertManager will send out an email notification or whatever type of notification is configured.   
   
It also takes care of deduplicating, grouping, & routing them to the correct receiver integration.   
   
## Configure AlertManager   
   
AlertManager is a separate component - it is not part of Prometheus server.   
   
It has it’s own configuration file.   
   
AlertManager has a simple UI deployed.   
   
`kubectl port-forward svc/monitoring-kube-prometheus-alertmanager -n monitoring 9093:9093 &`   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662782101/wiki/mrhhjwdt65emipjyolpw.png)   
   
It gives a read-only view of configuration as well as a way to filter the fired alerts.   
   
On the “status” tab you’ll find the global configuration - parameters valid in all other configuration contexts.   
   
The **receivers** are essentially notification integrations, that is how you tell AlertManager where to send the notifications. A “null” receiver means no notifications to be sent out.   
   
You can also tell AlertManager to send certain alerts to certain receivers and you can achieve this in “route” section.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662790067/wiki/vev67ikpbargbjdxmx6m.png)   
   
We use the “match” attribute matches expression with certain labels.   
   
```yaml
# alertmanager.yml

route:
  # When a new group of alerts is created by an incoming alert, wait at
  # least 'group_wait' to send the initial notification.
  # This way ensures that you get multiple alerts for the same group that start
  # firing shortly after another are batched together on the first
  # notification.
  group_wait: 10s

  # When the first notification was sent, wait 'group_interval' to send a batch
  # of new alerts that started firing for that group.
  group_interval: 30s

  # If an alert has successfully been sent, wait 'repeat_interval' to
  # resend them.
  repeat_interval: 30m

  # A default receiver
  receiver: "slack"

  # All the above attributes are inherited by all child routes and can
  # overwritten on each.
  routes:
    - receiver: "slack"
      group_wait: 10s
      match_re:
        severity: critical|warning
      continue: true

    - receiver: "pager"
      group_wait: 10s
      match_re:
        severity: critial
      continue: true

receivers:
  - name: "slack"
    slack_configs:
      - api_url: 'https://hooks.slack.com/services/XXXXXXXXX/XXXXXXXXX/xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        send_resolved: true
        channel: 'monitoring'
        text: "{{ range .Alerts }}<!channel> {{ .Annotations.summary }}\n{{ .Annotations.description }}\n{{ end }}"

  - name: "pager"
    webhook_configs:
      - url: http://a.b.c.d:8080/send/sms
        send_resolved: true
```
   
   
## Labs   
   
   
- [kubernetes.Prometheus Monitoring in K8s](../devlog/kubernetes.Prometheus%20Monitoring%20in%20K8s.md)   
- [prometheus.Prometheus Stack in Kubernetes](../devlog/prometheus.Prometheus%20Stack%20in%20Kubernetes.md)   
   
## Resources   
   
   
- [Awesome Prometheus alerts | Collection of alerting rules](https://awesome-prometheus-alerts.grep.to/rules.html)