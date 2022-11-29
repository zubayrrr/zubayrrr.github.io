---
created: 1658327416406
desc: ''
id: pr716orm61uub9wy1ksco8h
title: Automate Data Backup of EC2 instances
updated: 1658499723477
---
   
Related::  [boto](../devlog/boto.md), [aws.EC2](../devlog/aws.EC2.md), [AWS EBS](../devlog/AWS%20EBS.md)   
   
   
---   
   
**Premise**   
   
To create backup/snapshot volumes(storage) of all the EC2 instances.   
Volume snapshot is a copy of a volume.   
   
```py
import boto3
import schedule

ec2_client = boto3.client('ec2', region_name="eu-west-3")


def create_volume_snapshots():
    volumes = ec2_client.describe_volumes(
        Filters=[
            {
                'Name': 'tag:Name',
                'Values': ['prod']
            }
        ]
    )
    for volume in volumes['Volumes']:
        new_snapshot = ec2_client.create_snapshot(
            VolumeId=volume['VolumeId']
        )
        print(new_snapshot)


schedule.every().day.do(create_volume_snapshots)

while True:
    schedule.run_pending()
```
