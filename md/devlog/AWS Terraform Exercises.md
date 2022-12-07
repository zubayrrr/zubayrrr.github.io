---
category: '2022'
created: 2022-12-02 13:59:33.610000+00:00
id: caae1858-882f-407d-86d1-6576e996aa71
tags:
- devlog
title: AWS Terraform Exercises
updated: 2022-12-02 13:59:34.146000+00:00
---
   
## IAM AWS - Create a User   
   
As you probably know at this point, it's not recommended to work with the root account in AWS. For this reason you are going to create a new account which you'll use regularly as the admin account.   
   
1.  Create a user with password credentials   
2.  Add the newly created user to a group called "admin" and attach to it the policy called "Administrator Access"   
3.  Make sure the user has a tag called with the key `Role` and the value `DevOps`   
   
```terraform
# Create an IAM user named "devops-admin"
resource "aws_iam_user" "devops-admin" {
  name = "devops-admin"
}

# Create an IAM group named "admin"
resource "aws_iam_group" "admin" {
  name = "admin"
}

# Add the "devops-admin" user to the "admin" group
resource "aws_iam_group_membership" "admin" {
  name = "devops-admin"
  group = aws_iam_group.admin.name
}

# Attach the "Administrator Access" policy to the "admin" group
resource "aws_iam_group_policy_attachment" "admin" {
  group = aws_iam_group.admin.name
  policy_arn = "arn:aws:iam::aws:policy/AdministratorAccess"
}

# Create an IAM user password for "devops-admin"
resource "aws_iam_user_password" "devops-admin" {
  user = aws_iam_user.devops-admin.name
  password = "{your_password}"
}

# Add a tag to the "devops-admin" user with the key "Role" and value "DevOps"
resource "aws_iam_user_tag" "devops-admin" {
  user = aws_iam_user.devops-admin.name
  key = "Role"
  value = "DevOps"
}
```
   
   
## AWS IAM - Password Policy & MFA   
   
1.  Create password policy with the following settings:   
2.  At least minimum 8 characters   
3.  At least one number   
4.  Prevent password reuse   
5.  Then enable MFA for the account   
   
```terraform
# Create a password policy for the AWS account
resource "aws_iam_account_password_policy" "default" {
  minimum_password_length = 8
  require_numbers = true
  prevent_password_reuse = true
}

# Enable MFA for the "devops-admin" user
resource "aws_iam_user_mfa_device" "devops-admin" {
  user = aws_iam_user.devops-admin.name
  serial_number = "{your_mfa_device_serial_number}"
  authentication_code_1 = "{your_authentication_code_1}"
  authentication_code_2 = "{your_authentication_code_2}"
}
```
