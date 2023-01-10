---
created: 1655214348240
desc: ''
id: gualur07hbgjlaw396spiji
title: AWS CodeCommit
updated: 1655450869010
---
   
It is a version control service, which is hosted and fully managed(Unlike Github and Gitlab) by Amazon, which can be used to privately store data (documents, binary files, source code) and manage them in the cloud. It offers high scalability, security and helps manage source control service, which is used to host private Git repositories.   
   
It eliminates the requirement for the user to know Git and manage their own source control system or worry about scaling up or down their infrastructure. Codecommit supports all the standard functionalities that can be found in Git, which means it works effortlessly with user’s current Git-based tools. — via [What is AWS Codecommit?](https://www.knowledgehut.com/tutorials/aws/aws-codecommit)   
   
It integrates well with other services ([AWS CodeDeploy](../devlog/AWS%20CodeDeploy.md), [AWS CodeBuild](../devlog/AWS%20CodeBuild.md), [AWS CodePipeline](../devlog/AWS%20CodePipeline.md), [AWS Lambda](../devlog/AWS%20Lambda.md), [AWS SNS](/not_created.md)).   
   
## Creating a repository   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655274009/wiki/mkc6bm8oka3kwfrjncen.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655273410/wiki/n419mau6b1vl7llmeq0d.png)   
   
   
- You’ll need to choose a user on [aws.IAM](../devlog/aws.IAM.md) that you want to give access to AWS CodeCommit.   
  - **Add Permissions** on Permissions tab   
  - **Grant Permissions** choose **Attach existing policies directly**   
  - Select **AWSCodeCommitFullAccess**   
- Select the user from AWS IAM on Security Credentials tab   
  - Generate **HTTPS Git credentials for AWS CodeCommit**   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1655273772/wiki/expmhzqs48qypcd0abeg.png)   
  - Download the credentials   
- Clone the repository using the URL.   
   
## CodeCommit repository actions using [AWS CLI](../devlog/aws%20cli.md)   
   
   
- Create - `aws codecommit create-repository --repository-name My-repo`   
- View - `aws codecommit get-repository --repository-name My-repo`   
- List - `aws codecommit list-repositories`   
- Delete - `aws codecommit delete-repository --repository-name My-repo`   
   
You’ll need Access Key ID, Secret Access Key token to be able to interact with CodeCommit repository.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655446842/wiki/eh6bwxpaa5a4bc4autgb.png)   
   
As for cloning, committing, pulling, pushing you can use the usual [version control.git](../devlog/version%20control.git.md) commands.   
   
## CodeCommit Data Security   
   
   
- For encryption in transit and at rest it uses [AWS KMS](../devlog/AWS%20KMS.md).   
  - When you create a CodeCommit repository AWS creates an encrypted key. In [aws.IAM](../devlog/aws.IAM.md), you can find that key. These are by region keys.   
  - AWS managed keys.   
- You can add Deny policies.   
- To restrict creation and deletion of repositories:   
  - Add policy such as **AWS CodeCommit PowerUser** or create an IAM group and add the policy to the group and put all your developers to that group.   
- For admins you could have **AWS CodeCommit FullAccess** policy   
- You could add more granular policies such as limiting push capabilities.