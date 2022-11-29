---
created: 1662771416615
desc: ''
id: rhoxvv3etzc4xfqr379u9dh
title: Grafana
updated: 1662771451381
---
   
The default credentials are:   
   
user: Admin   
password: prom-operator   
   
In Grafana, you work with Dashboards.   
   
Dashboards are configured by default in our setup.   
   
Dashboards are organized in folders.   
   
They’re a set of one or more panels. You can create your own dashboards. Organized into one or more rows. Rows are used to group panels together.   
   
**Panel**   
   
   
- It is the basic visualization building block in Grafana.   
- Composed by a query and a visualization.   
- Each panel has a query editor specific to the data source selected in the panel.   
- Can be moved and resized within a dashboard.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662770434/wiki/yqdadrexfbblowrr31hy.png)   
   
Right click on a panel and select “edit” to find a view for PromQL query.   
   
Using PromQL you can query data from Prometheus and have Grafana visualize it for you.   
   
## Create your own dashboards   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662771519/wiki/e2pkhaafhrhj3zbr1sju.png)   
   
You’ll need to write PromQL query or select from metrics browser.   
   
You can customize the dashboard with different options.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662771619/wiki/ozqb7u8yxkmatuvvmi8h.png)   
   
## Resource consumption   
   
The “Nodes” dashboard will visualize the CPU, Memory. Storage usage of your cluster per node.   
   
## Test anomaly    
   
Produce a spike by hitting the cluster endpoint repeatedly.   
   
`kubectl run curl-test --image=radial/busyboxplus:curl -i --tty -rm` will give access to the pod.   
   
`kubectl get svc` to get endpoint.   
   
```bash
#!/bin/sh
for i in $(seq 1 10000)
do
	curl <endpoint> > output.txt
done
```
   
   
`chmod +x test.sh`   
   
`./test.sh`   
   
Check the dashboard for spike in CPU usage.   
   
## Configure Users & Data sources   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662772195/wiki/y42gael7cieptsyejnus.png)   
   
The Prometheus endpoint is configured in Grafana under “Data sources”.   
   
Grafana supports many different storage backends(data sources).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662772348/wiki/zcap37xr4ay294f9wwyz.png)