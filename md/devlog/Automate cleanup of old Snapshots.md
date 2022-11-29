---
created: 1658499418278
desc: ''
id: 6yea3nujt8yupmf4wdtj7mk
title: Automate cleanup of old Snapshots
updated: 1658499731869
---
   
Related::  [boto](../devlog/boto.md), [Automate Data Backup of EC2 instances](../devlog/Automate%20Data%20Backup%20of%20EC2%20instances.md), [AWS EBS](../devlog/AWS%20EBS.md)   
   
   
---   
   
**Premise**   
   
If we have a scheduler creating a lot of snapshots everyday, we need a way of cleaning up those old snapshots. We can schedule a new job for cleaning old snapshots every week/month.   
   
```py
import boto3
from operator import itemgetter

ec2_client = boto3.client('ec2', region_name="eu-west-3")

volumes = ec2_client.describe_volumes(
    Filters=[
        {
            'Name': 'tag:Name',
            'Values': ['prod']
        }
    ]
)

for volume in volumes['Volumes']:
    snapshots = ec2_client.describe_snapshots(
        OwnerIds=['self'],
        Filters=[
            {
                'Name': 'volume-id',
                'Values': [volume['VolumeId']]
            }
        ]
    )

    sorted_by_date = sorted(snapshots['Snapshots'], key=itemgetter('StartTime'), reverse=True)

    for snap in sorted_by_date[2:]:
        response = ec2_client.delete_snapshot(
            SnapshotId=snap['SnapshotId']
        )
        print(response)
```
