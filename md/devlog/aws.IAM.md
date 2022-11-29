---
created: 1655017676616
desc: ''
id: uu932tw90r0gvvg8maqr3s1
title: IAM
updated: 1664905903063
---
   
   
- AWS Identity and Access Management (IAM), is a service that allows AWS customers to manage user access and permissions for their accounts, and available APIs/services within AWS. IAM can manage users, security credentials (such as API access keys), and allow users to access AWS resources.   
- You can create users and groups and set permissions on both of them to either allow or deny access to AWS resources via use of policies.   
- IAM is free and included in every AWS account.   
- 2 main features of IAM are Users and Roles.   
   
IAM components are **Global**, they are not created in a particular region but are specified for a whole account.   
   
## Authorization vs Authentication   
   
Authentication and authorization are two vital information security processes that administrators use to protect systems and information. **Authentication verifies the identity of a user or service**, and **authorization determines their access rights**.   
   
## Root User   
   
There are two different types of users in AWS. You are either the account owner (root user) or you are an AWS Identity and Access Management (IAM) user. The root user is created when the AWS account is created. IAM users are created by the root user or an IAM administrator for the account.   
   
It is not recommended to use Root User for day-to-day activities, you'd instead create and use an IAM User.   
   
### IAM Users   
   
   
- Once you create an AWS account you're given Root user access, this is the main account you log into your AWS resources with. It has unlimited privileges.   
- With Root user you can create an IAM user, another name for a username and password that can log into your AWS account, but you decide who gets access to what.   
- With IAM you can create specific policies to define what a user can access, you can also add users to a group, to which policies can be applied making it easier.   
- You can create a group that has access to your development servers and then add all the developers to that group.   
- In addition to human users, you can also have system users on AWS. For example, you can have [jenkins](../devlog/jenkins.md) that deploys [Docker](../devlog/docker.md) container on [aws.EC2](../devlog/aws.EC2.md) instance or [Jenkins](../devlog/jenkins.md) that pushes Docker images to AWS Docker Repo called [AWS ECR](/not_created.md).   
- It is a good practice to assign permissions/policies to a group and then add the user to the group.   
   
### IAM Policy Example: Admin User   
   
IAM has both, a visual editor and a JSON editor.   
   
Example of Admin policy in JSON editor:   
   
```json
{
  "Version": "2012-01-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}
```
   
   
### IAM Roles   
   
   
- They allow you to delegate access to a user or a service, roles differ from users in a way that not only users can assume a role but also services can assume a role as well.   
- Basically delegating AWS Services to other AWS Services.   
- Its an extra layer of security above just the usual username, password and firewalls.   
- Example of a role: a website can assume a role that has access to your Database.   
- Roles can also allow other users from different AWS accounts to use a resource in your AWS account.   
   
### IAM Users VS IAM Roles   
   
   
- Users are assigned to human users or system users.   
- Policies cannot be assigned to AWS Services directly. Instead, you can assign a role to a service and then assign a policy to that role.   
- There are roles for each service. Roles have permissions/policy attached to it.   
- Whenever you create a role:   
  - Assign that role to an AWS Service.   
  - Attach policies to that role.   
   
## Labs   
   
[aws.IAM.creating IAM User and Group](/not_created.md)