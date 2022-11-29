---
created: 1658501105422
desc: ''
id: 9im04y0czc0iiw0jw0rbr92
title: Restore volume from a snapshot of EC2 instance
updated: 1658501302748
---
   
Related::  [boto](../devlog/boto.md), [aws.EC2](../devlog/aws.EC2.md)   
   
   
---   
   
**Premise**   
   
Say that one of our EC2 instance's volume gets corrupted but we want to restore it using one of the snapshots that we've made [Automate Data Backup of EC2 instances](/not_created.md).   
   
```py
import boto3
from operator import itemgetter

ec2_client = boto3.client('ec2', region_name="eu-west-3")
ec2_resource = boto3.resource('ec2', region_name="eu-west-3")

instance_id = "i-04f01be7a765eaf7e"

volumes = ec2_client.describe_volumes(
    Filters=[
        {
            'Name': 'attachment.instance-id',
            'Values': [instance_id]
        }
    ]
)

instance_volume = volumes['Volumes'][0]

snapshots = ec2_client.describe_snapshots(
    OwnerIds=['self'],
    Filters=[
        {
            'Name': 'volume-id',
            'Values': [instance_volume['VolumeId']]
        }
    ]
)

latest_snapshot = sorted(snapshots['Snapshots'], key=itemgetter('StartTime'), reverse=True)[0]
print(latest_snapshot['StartTime'])

new_volume = ec2_client.create_volume(
    SnapshotId=latest_snapshot['SnapshotId'],
    AvailabilityZone="eu-west-3b",
    TagSpecifications=[
        {
            'ResourceType': 'volume',
            'Tags': [
                {
                    'Key': 'Name',
                    'Value': 'prod'
                }
            ]
        }
    ]
)

while True:
    vol = ec2_resource.Volume(new_volume['VolumeId'])
    print(vol.state)
    if vol.state == 'available':
        ec2_resource.Instance(instance_id).attach_volume(
            VolumeId=new_volume['VolumeId'],
            Device='/dev/xvdb'
        )
        break
```
