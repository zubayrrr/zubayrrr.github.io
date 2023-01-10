---
created: 1661344554557
desc: ''
id: nrg9wym2sf89qemcdsra2ab
title: Dynamic Inventory
updated: 1661424678114
---
   
**Overview**   
   
   
- Let's create 3 EC2 instances with [terraform](../devlog/terraform.md)   
- Connect to these servers with Ansible without hardcoding the IP address.   
   
**Inventory Plugin vs Inventory Script**   
   
In our Ansible code we need the functionality to connect to our AWS account, fetch server information. For this we've dynamic inventory scripts and plugins. Ansible recommends using plugins over scripts. Because plugins can use the state management of Ansible. Plugins are written in [languages.YAML](../devlog/languages.YAML.md). Scripts are written in Python.   
   
   
- There are different plugins/scripts for different infrastructure provider.   
- `ansible-doc -t inventory -l` to list all available plugins.   
- We'll use the AWS plugin in our case.   
   
**`aws_ec2` Plugin**   
   
   
- The prerequisites of using the plugin is that you need [boto](../devlog/boto.md)3 and `botocore` installed on your local machine.   
- Enable the plugin inside `ansible.cfg` like `enable_plugins = aws_ec2`.   
- Create a config file named `inventory_aws_ec2.yaml`, `.yaml`is required.   
   
```yaml
# inventory_aws_ec2.yaml
---
plugin: aws_ec2
regions:
  # get all hosts from specific region(s)
  - eu-west-3
```
   
   
   
- `ansible-inventory` to display or dump the configured inventory as Ansible sees it.   
  - `ansible-inventory -i inventory_aws_ec2.yaml --list`   
  - `ansible-inventory -i inventory_aws_ec2.yaml --graph`   
   
**Assign public DNS to EC2 instances**   
   
The `ansible-inventory ...` command will return a list **private** DNS names. We cannot use these to connect to them. We need to assign them **public** DNS names if we want to interact with it from outside the VPC(where the servers live).   
   
In the [Terraform](../devlog/terraform.md) code:   
   
```t
resource "aws_vpc" "myapp-vpc" {
  cidr_block = var.vpc_cidr_block
  enable_dns_hostnames = true
  tags = {
      Name = "${var.env_prefix}-vpc"
  }
}
```
   
   
**Configure Ansible to use dynamic inventory**   
   
In the Ansible code, set the `hosts:` to either `all` or `aws_ec2`. You also need private key and user. Like:   
   
```cfg
remote_user = ec2-user
private_key_file=~/.ssh/id_rsa
```
   
   
Run the playbook:   
   
`ansible-playbook -i inventory_aws_ec2.yaml deploy-app.yaml`   
   
You can also make the `inventory_aws_ec2.yaml` as the default host file inside the `ansible.cfg` file. Like: `inventory = inventory_aws_ec2.yaml`.   
   
**Target only specific servers**   
   
What if you wanted to target only specific servers. In the plugin configuration, you can use `filters` to filter the servers you want to use. The same filter attributes that are used by [aws cli](../devlog/aws%20cli.md). In our case, let's use the tag name.   
   
```yaml
filters:
  tag:Name: dev*
  instance-state-name: running
```
   
   
**Create dynamic groups**   
   
You can group different servers in the plugin configuration file.   
   
Example: grouped by tag.   
   
```yaml
---
plugin: aws_ec2
regions:
  - eu-west-3
keyed_groups:
  - key: tags
    prefix: "tag"
  # the values/attributes used here are from the output of `ansible-inventory ...` not the same attributes as `filters`
```
   
   
You can select the tag name and use it as the `hosts:` value in the Ansible code.   
   
Example: group by instance type   
   
```yaml
---
plugin: aws_ec2
regions:
  - eu-west-3
keyed_groups:
  - key: tags
    prefix: "tag"
  - key: instance_type
    prefix: instance_type
```
