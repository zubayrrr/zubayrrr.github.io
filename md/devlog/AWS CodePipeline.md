---
created: 1655279577657
desc: ''
id: 3n1o179sti2wtnjkq48one1
title: AWS CodePipeline
updated: 1655544289217
---
   
AWS CodePipeline is a completely managed continuous delivery service(with manual approval) that assists you in automating your release pipelines for quick and reliable application and infrastructure changes.   
   
Based on the release model you set, CodePipeline automates the build, test, and deploy parts of your release process every time there is a code change. This allows you to provide features and upgrades quickly and consistently. AWS CodePipeline can be easily integrated with third-party services like GitHub or your own custom plugin. You only pay for what you use with AWS CodePipeline. There are no hidden costs or long-term obligations. — via [AWS CodePipeline - Coding Ninjas CodeStudio](https://www.codingninjas.com/codestudio/library/aws-codepipeline)   
   
   
- Automatic   
  - From the check-in of your code to the deployment on to your servers, CodePipeline takes care of the entire process.   
- Easy to setup   
  - CodePipeline has no servers to provision, it's dead simple to configure and get working. There are pre-built plugins or you can roll your own.   
- Configurable   
  - You can create, configure and modify all stages of your software release process with ease. You can implement automated testing and customize the deployment process.   
   
CodeCommit is not the only repository you can use with [AWS CodePipeline](../devlog/AWS%20CodePipeline.md), such as [aws.S3](../devlog/aws.S3.md), Github, Bitbucket and Github Enterprise.   
   
   
- You need an [aws.IAM](../devlog/aws.IAM.md) user with right policies attached to it.   
   
Create Pipeline   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655279967/wiki/cavxaueres9g0y82ejum.png)   
   
Unlike [AWS CodeDeploy](../devlog/AWS%20CodeDeploy.md) it supports [AWS CodeCommit](../devlog/AWS%20CodeCommit.md) so you can choose your Source as such.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655280066/wiki/ofw8mz5jopulafyhazzk.png)   
   
You can use [aws.S3](../devlog/aws.S3.md) as a source too with change detection options.   
   
You can add a build stage if your application requires compiling or you can skip to deploy stage.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655540479/wiki/ehjwkvx8qcvu0dxznclg.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655280123/wiki/kduzm8nljigeq2dupxos.png)   
   
## Code Pipeline with [AWS CodeBuild](../devlog/AWS%20CodeBuild.md)   
   
CodeBuild can be used in both build and test stages of a pipeline. You can add CodeBuild build action to a pipeline as well as CodeBuild test action.   
   
## Versioning   
   
CodePipeline uses the ETag to manage and understand the flow so far for that execution of the pipeline. CodePipeline can have multiple executions at the same time. So, it needs to have a way to identify when version of the artifact is tied to which execution.   
   
## Managing CodePipeline   
   
   
- View logs for debugging   
- Edit/Add Stages -> Action providers   
- Toggle transitions   
- Retry failed stages   
- Delete   
   
## Approval Action   
   
   
- Setup approvers in [aws.IAM](../devlog/aws.IAM.md) via managed policy: **AWSCodePipelineApproverAccess** (from Action Provider in a stage)   
   
## CodePipeline with [AWS EventBridge](../devlog/AWS%20EventBridge.md)   
   
   
- Events can come from multiple stages within the pipeline.   
- EventBridge can watch over events and trigger [AWS SNS](/not_created.md) topic based on it.   
- EventBridge can work with [AWS Lambda](../devlog/AWS%20Lambda.md) at source stage. It can work with SNS at the build or deploy stages.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655544508/wiki/rvmsyahweeycgtzonaav.png)