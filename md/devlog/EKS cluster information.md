---
created: 1658326654730
desc: ''
id: llkdoaituan5psfnwiw8tf5
title: EKS cluster information
updated: 1658326766477
---
   
Related::  [boto](../devlog/boto.md), [aws.EKS](../devlog/aws.EKS.md)   
   
   
---   
   
**Premise**   
   
We want to get our EKS Cluster info like:   
   
   
- Cluster Status   
- Which [Kubernetes](../devlog/kubernetes.md) version?   
- Cluster Endpoint   
   
```py
import boto3

client = boto3.client('eks', region_name="eu-west-3")
clusters = client.list_clusters()['clusters']

for cluster in clusters:
    response = client.describe_cluster(
        name=cluster
    )
    cluster_info = response['cluster']
    cluster_status = cluster_info['status']
    cluster_endpoint = cluster_info['endpoint']
    cluster_version = cluster_info['version']

    print(f"Cluster {cluster} status is {cluster_status}")
    print(f"Cluster endpoint: {cluster_endpoint}")
    print(f"Cluster version: {cluster_version}")
```
