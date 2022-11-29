---
created: 1658323453941
desc: ''
id: 890e29fylut7y1zqv9mtw7n
title: Add Env Tags to  Ec2 Servers with Boto3
updated: 1658326689585
---
   
Related::  [boto](../devlog/boto.md), [aws.EC2](../devlog/aws.EC2.md)   
   
   
---   
   
**Premise**   
   
We've a few prod servers in one region and a few dev servers in another region. They were created using Terraform. We want to add corresponding environment "dev", "prod" tags to these servers.   
   
```py
import boto3

ec2_client_paris = boto3.client('ec2', region_name="eu-west-3")
ec2_resource_paris = boto3.resource('ec2', region_name="eu-west-3")

ec2_client_frankfurt = boto3.client('ec2', region_name="eu-central-1")
ec2_resource_frankfurt = boto3.resource('ec2', region_name="eu-central-1")

instance_ids_paris = []
instance_ids_frankfurt = []

reservations_paris = ec2_client_paris.describe_instances()['Reservations']
for res in reservations_paris:
    instances = res['Instances']
    for ins in instances:
        instance_ids_paris.append(ins['InstanceId'])


response = ec2_resource_paris.create_tags(
    Resources=instance_ids_paris,
    Tags=[
        {
            'Key': 'environment',
            'Value': 'prod'
        },
    ]
)

reservations_frankfurt = ec2_client_frankfurt.describe_instances()['Reservations']
for res in reservations_frankfurt:
    instances = res['Instances']
    for ins in instances:
        instance_ids_frankfurt.append(ins['InstanceId'])


response = ec2_resource_frankfurt.create_tags(
    Resources=instance_ids_frankfurt,
    Tags=[
        {
            'Key': 'environment',
            'Value': 'dev'
        },
    ]
)
```
