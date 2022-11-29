---
created: 1653408519142
desc: ''
id: e7pods321uz4fxgzzdhf002
title: Boto
updated: 1658505846946
---
   
Topics::  [aws](../devlog/aws.md), [languages.python](../devlog/languages.python.md)   
   
   
---   
   
Boto3 is the name of the Python SDK for AWS. It allows you to directly create, update, and delete AWS resources from your Python scripts.   
   
## Automation on AWS using Boto   
   
   
- Infrastructure provisioning just like [terraform](../devlog/terraform.md)   
- Making backups   
- Doing cleanups   
- Configuration of existing servers   
- Doing health-checks/monitoring   
   
1. Connect to AWS account (uses `~/.aws/config` that was created using `aws configure` )   
2. Create a VPC   
3. Create a Subnet   
   
`pip install boto3` to install the library on your local machine   
   
```py
# main.py
import boto3

ec2_client = boto3.client('ec2')
# overriding default region configured on ~/.aws/config
# ec2_client = boto3.client('ec2', region_name="eu-central-1")

ec2_resource = boto3.resource('ec2')

new_vpc = ec2_resource.create_vpc(
  CidrBlock="10.0.0.0/16"
)

new_vpc_create_subnet(
  CidrBlock="10.0.0.0/24"
)

new_vpc.create_tags(
  Tags=[
    {
      'Key': 'Name',
      'Value': 'my-vpc
    },
  ]
)

all_available_vpcs = ec2_client.describe_vpcs()
vpcs = all_available_vpcs["Vpcs"]
print(all_available_vpcs)

for vpc in vpcs:
  print(vpc["VpcId"])
  cidr_block_assoc_sets = vpc["CidrBlockAssociationSet"]
  for assoc_set in cidr_block_assoc_sets:
      print(assoc_set["CidrBlockState"])
```
   
   
## Notes   
   
**How to use `boto3`**   
   
   
- What function name we need to call?   
- What parameters the function takes?   
- What is returned from this function call? (**response**) (**response datatype**)   
   
**`client` VS `resource`**   
   
   
- Client is more low-level API.   
- Client provides one-to-one mapping to the underlying HTTP API operations.   
   
   
- Resource provides resource objects to access attributes and perform actions.   
- Resource is like a wrapper around Client that makes it a higher-level API and object-oriented.   
- Resource returns a `Resource Object`, we can use for subsequent calls.   
   
**Terraform VS Python**   
   
   
- [terraform](../devlog/terraform.md) manages state of the infrastructure. It creates and configures.   
- Since Terraform knows the current state, it also knows the different between current state and desired state. It takes care of all the decision/steps to be made.   
- Terraform is idempotent(no surprises).   
- If you delete the code block of a resource declaration and do `terraform apply` it'll delete the resource as it knows that you no longer want those resource based on your TF configuration file.   
   
   
- Python is not idempotent, it'll create infrastructure every time you run the script. You're not "declaring" how many "resources" you want in your infra. Basically, it doesn't have state.   
- You need to explicitly delete your resources. Not easy because of specific policies(like of a VPC). Requires a lot of code to make it happen.   
   
**Use cases of Boto**   
   
   
- More complex logic, since Python is a full fledged programming language allowing you to use conditional statements etc.   
- Boto allows far more things than Terraform offers because of it's low-level API.   
- Boto is an AWS library - it offers far more information than Terraform. Allowing you to do things like backups, monitoring, scheduled tasks etc.   
- You can use other libraries in your program to extend functionality.   
- You can even add a web interface to your program. A UI.   
   
## Labs   
   
   
- [ec2 server status check](../devlog/ec2%20server%20status%20check.md)   
- [add env tags to  ec2 servers](../devlog/add%20env%20tags%20to%20%20ec2%20servers.md)   
- [EKS cluster information](../devlog/EKS%20cluster%20information.md)   
- [Automate Data Backup of EC2 instances](../devlog/Automate%20Data%20Backup%20of%20EC2%20instances.md)   
- [Automate cleanup of old Snapshots](../devlog/Automate%20cleanup%20of%20old%20Snapshots.md)   
- [Restore volume from a snapshot of EC2 instance](../devlog/Restore%20volume%20from%20a%20snapshot%20of%20EC2%20instance.md)   
   
## Resources   
   
   
- [Boto3 documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)