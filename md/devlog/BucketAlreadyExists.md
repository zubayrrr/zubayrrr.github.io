---
category: '2022'
created: 2022-12-02 23:46:57.969000+00:00
id: 7ac1dc6d-211a-4630-ac77-3b72055cc35a
tags:
- devlog
title: BucketAlreadyExists
updated: 2022-12-02 23:46:58.665000+00:00
---
   
Topics:: [aws.S3](../devlog/aws.S3.md)   
   
   
---   
If you receive the error `BucketAlreadyExists` when trying to create a new S3 bucket, it means that the bucket name you chose is already in use by another user. S3 bucket names are unique across all users of the system, so you'll need to choose a different bucket name and try again.   
   
Here are a few tips for choosing a unique bucket name:   
   
1.  Use a combination of your organization's name and a descriptive term related to the bucket's contents. For example, `mycompany-documents` or `mycompany-images`.   
       
2.  Include a unique identifier in the bucket name. This could be a random string of numbers or letters, or the current date or time. For example, `mycompany-documents-20221202` or `mycompany-images-rnd123`.   
       
3.  Avoid using common words or terms that are likely to be used by other users. For example, "bucket" or "aws" are commonly used words that may already be in use.   
       
   
Once you've chosen a unique bucket name, you can use the `aws s3 mb` command to create the new bucket. Here's an example of how to use this command:   
   
   
`aws s3 mb s3://my-unique-bucket-name`   
   
If you're using Terraform to manage your S3 buckets, you can also update your Terraform configuration to reflect the new bucket name and use the `terraform apply` command to create the new bucket.