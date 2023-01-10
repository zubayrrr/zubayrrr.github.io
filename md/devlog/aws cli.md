---
created: 1661078349631
desc: ''
id: d9jtwzd79ztz3t93m5ibhj6
title: AWS CLI
updated: 1664911245382
---
   
You use AWS Cli if you want programmatic access to your AWS resources. You can execute commands from other AWS services.   
   
The AWS Cli is a very powerful command line tool. It provides commands for every AWS service and resources. Anything you can do with AWS Console can be achieved using the AWS Cli. It is also generally much easier to use AWS via the Cli than it is using the UI.   
   
## Install and Configure   
   
   
- [Installing or updating the latest version of the AWS CLI - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)   
- The default configuration is stored `~/.aws/config` and user credentials are stored in `~/.aws/credentials`.   
- The access to AWS is configured through an Access ID and Secret Access Key(which is created from the console).   
- `aws configure` to start configuring the Cli.   
- The default output format refers to the output(return) that AWS gives after running a command. This can be set as `json`.   
   
## Command Structure   
   
`aws <command> <subcommand> [options and parameters]`   
   
   
- `aws` = the base call to the AWS Cli program.   
- `command` = the AWS service   
- `subcommand` = specifies which operation to perform.   
   
Examples:   
   
   
- `aws ec2 help`   
- `aws iam help`   
   
```bash
# launch ec2 instance in the specified subnet of a VPC
aws ec2 describe-subnets
aws ec2 describe-instances # -> will give us ami-imageid, we will use the same one
aws ec2 run-instances \
    --image-id ami-xxxxxxxx \
    --count 1 \ # how many instances to launch
    --instance-type t2.micro \
    --key-name MyKeyPair \ # pem file, you can reuse thats already created or create a new one
    --security-group-ids sg-903004f8 \ # reuse already created or create a new one
    --subnet-id subnet-6e7f829e
```
   
   
## Create an EC2 Instance   
   
Steps:   
   
   
- Create a security group.   
- Create an [SSH](../devlog/ssh.md) key pair (to SSH into the created EC2 instance).   
- Create a EC2 instance.   
   
Let's start with creating a security group:   
   
   
- `aws ec2 describe-security-groups` - list all security groups   
   
> Since security group needs to be created inside a VPC, we need a VPC ID to create a new security group.   
   
   
- `aws ec2 describe-vpcs` - get all existing VPCs   
- `aws ec2 create-security-group --group-name my-sg --description "my security group" --vpc-id <vpc id>` - create a new security group.   
- `aws ec2 describe-security-groups --group-ids <security group id>` - get info on an existing SG with ID.   
   
> Configure firewall rules   
   
```bash
aws ec2 authorize-security-group-ingress \
--group-id <SG id> \
--protocol tcp \
--port 22 \
--cidr <IP addr>  # source, check your IP address, who can access
```
   
   
By default security group has outbound permissions to all destinations.   
   
> Create Key pair   
   
```
aws ec2 create-key-pair \
--key-name MyKPCli \
--query 'KeyMaterial' \ # gives unencrypted pem
--output text > MyKPCli.pem
```
   
   
> Get image-id, subnet-id   
   
   
- `aws ec2 describe-subnets` grab it either from the console or using this command   
- `aws ec2 ` grab it from the console, from the list of AMIs   
   
> Create an EC2 instance   
   
```bash
aws ec2 run-instances \
    --image-id ami-xxxxxxxx \
    --count 1 \
    --instance-type t2.micro \
    --key-name MyKPCli \
    --security-group-ids <SG ID> \
    --subnet-id <subnet ID>
```
   
   
> Grab public IP so you can SSH into it   
   
`aws ec2 describe-instances` list all instances in your region, grab the public IP from the output.   
   
> Change permissions of the .pem file   
   
   
- `ls -l MyKPCli.pem` get info on permission of this file.   
- `chmod 400 MyKPCli.pem` to modify the permissions to restrict it to only your user.   
  - Read access only for the owner.   
   
> SSH into the machine   
   
`ssh -i MyKPCli.pem ec2-user@<public-ip>`   
   
   
---   
   
## Filter & Query   
   
**Filter** and **Query** - describe command's option   
   
`aws <command> describe-` helps you with listing certain components of a resource etc.   
   
You can chain a filter to this command to filter **certain components/resource**.   
   
You can also query(s) filter attributes of a filtered **component's specific attributes**.   
   
**Examples**:   
   
```bash
aws ec2 describe-instances \
--filters "Name=instance-type, Values=t2.micro" \
--query "Reservations[].Instances[].InstanceId"
```
   
   
Even tags can also be filtered.   
   
```bash
aws ec2 describe-instances --filters "Name=tag:Type,Values=Web Server with Docker"
```
   
   
OR   
   
```bash
aws ec2 describe-instances \
--filters "Name=tag:Type,Values=Web Server with Docker" \
--query "Reservations[].Instances[].InstanceId"
```
   
   
   
---   
   
## Using IAM Command   
   
Create User, Group and assign permissions.   
   
> Create a group   
   
`aws iam create-group --group-name MyGroupCli` - the group names should sufficiently descriptive.   
   
ARN = Amazon Resource Name; to uniquely identify a component/resource. It is basically a unique **identifier**.   
   
> Create a user   
   
`aws iam create-user --user-name MyUserCli`   
   
> Add user to group   
   
`aws iam add-user-to-group --user-name MyUserCli --group-name MyGroupCli`   
   
> Get group info   
   
`aws iam get-group --group-name MyGroupCli`   
   
> Get policy ARN   
   
A policy is basically a **group of permissions**.   
   
**From Console**:   
   
Go to the IAM, click on "Policies" on the left sidebar. Click a policy to open it's summary page. Copy the **Policy ARN**.   
   
**From Cli**:   
   
You need to know the name of the policy.   
   
```bash
aws iam list-policies \
--query 'Policies[?PolicyName==`AmazonEC2FullAccess`].{ARN:arn}'
--output text
```
   
   
> Assign permissions to group   
   
Permissions can be assigned directly to a user but if you've a group of users that need same permissions it makes sense to group the users into a group and assign the permissions directly to the group.   
   
   
- `aws iam attach-user-policy`   
- `aws iam attach-group-policy`   
   
```bash
aws iam attach-group-policy \
--group-name MyGroupCli \
--policy-arn arn:aws:iam::aws:policy/AmazonEC2FullAccess
```
   
   
> Validate policy attachment   
   
```bash
aws iam list-attached-group-policies \
--group-name MyGroupCli
```
   
   
## Create Credentials   
   
**For new User**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661087467/wiki/zvzaf7d2terov8xv4owm.png)   
   
When creating a user from the console you can setup all kinds of credentials/permissions for the user.   
   
How do we do that same with the Cli?   
   
> Assign a password   
   
```bash
aws iam create-login-profile \
--user-name MyUserCli \
--password myPwd123Test \ # password needs to be strong
--password-reset-required # make user reset password on first login
# iam:ChangePassword policy needs to be attached to allow the user to change password
```
   
   
> Get user info   
   
`aws iam get-user --user-name MyUserCli` - `Account ID or ARN` will be required for the user login(Sign in as IAM User).   
   
## Create and Assign Custom Policy   
   
A custom policy for a user/group needs to be defined in a `.json` file.   
   
```json
// changePwdPolicy.json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iam:GetAccountPasswordPolicy",
      "Resource": "**"
    },
    {
      "Effect": "Allow",
      "Action": "iam:ChangePassword",
      "Resource": "arn:aws:iam::<12-digit-account-id:user/${aws:username}"
    }
  ]
}
```
   
   
**Creating the policy**:   
   
```bash
aws iam create-policy \
--policy-name changePwd \
--policy-document file://changePwdPolicy.json
```
   
   
Copy the ARN of the policy from the output.   
   
**Assigning policy to user group**:   
   
```bash
aws iam attach-group-policy \
--group-name MyGroupCli \
--policy-arn <copied-policy-arn>
```
   
   
## Create Access keys   
   
**For new User**   
   
```bash
aws iam create-access-key --user-name MyUserCli
```
   
   
Copy the `AccessKeyId` and `SecretAccessKey` from the output in order to login as that user from the Cli (programmatic access).   
   
## Switch User   
   
**In the Cli**   
   
There are 3 ways of switching the user in the Cli:   
   
1. `aws configure` to overwrite `~/.aws/` which was set previously.   
2. Use `aws configure set` to overwrite only the credentials.   
   
   - `aws configure set aws_access_key_id <access-key>`   
3. Set bash [environment variable](../devlog/environment%20variable.md)s to temporarily switch a user. It will automatically use the new credentials in that session(terminal).   
   
   - `export AWS_ACCESS_KEY_ID=<access-key>`   
   - `export AWS_SECRET_ACCESS_KEY=<secret-key>`   
   - Optionally you can also change your default region using `AWS_DEFAULT_REGION`   
   
## Delete Resources   
   
`aws ec2 delete-` commands to delete your EC2 resources.   
   
## Profiles   
   
A named profile is a collection of settings and credentials that you can apply to a AWS CLI command. When you specify a profile to run a command, the settings and credentials are used to run that command. Multiple named profiles can be stored in the config and credentials files.   
   
See also: [terraform](../devlog/terraform.md) :)   
   
## Examples   
   
```bash
aws ec2 describe-instances --query "Reservations[].Instances[].{InstanceId:InstanceId,PublicIP:PublicIpAddress,PrivateIP:PrivateIpAddress,Location:Placement.AvailabilityZone,Name:Tags[?Key=='Name']|[0].Value,Type:InstanceType,Status:State.Name,VpcId:VpcId, MAC:NetworkInterfaces[0].MacAddress, OS:PlatformDetails,DNS:PrivateDnsName}" --filters Name=instance-state-name,Values=running --output table
```
   
   
The `aws ec2 describe-instances` command is used to list information about Amazon Elastic Compute Cloud (EC2) instances.   
   
The `--query` option allows you to specify a JMESPath query to filter the results. The query provided in the example will return the following information for each instance:   
   
   
-   `InstanceId`: the ID of the instance   
-   `PublicIP`: the public IP address of the instance   
-   `PrivateIP`: the private IP address of the instance   
-   `Location`: the availability zone in which the instance is located   
-   `Name`: the name of the instance (as specified by the 'Name' tag)   
-   `Type`: the type of instance (e.g. t2.micro)   
-   `Status`: the current status of the instance (e.g. running)   
-   `VpcId`: the ID of the virtual private cloud (VPC) in which the instance is located   
-   `MAC`: the MAC address of the instance   
-   `OS`: the operating system of the instance   
-   `DNS`: the private DNS name of the instance   
   
The `--filters` option is used to filter the results based on the specified criteria. In this case, the command will only return instances with a `Name` of `instance-state-name` and a `Values` of `running`.   
   
The `--output` option allows you to specify the format in which the results should be output. In this case, the results will be output in a table format.   
   
## Resources   
   
   
- [aws — AWS CLI 2.8.0 Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html)