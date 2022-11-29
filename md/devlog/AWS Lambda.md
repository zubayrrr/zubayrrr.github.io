---
created: 1655018320878
desc: ''
id: etxu35hmga4ee3p1w1kxj9o
title: AWS Lambda
updated: 1661870070410
---
   
It is a compute service that lets you run code without having to install it on the operating system/provision a server. [serverless](../devlog/serverless.md). Lambda is stateless. It is event driven. It is a function that is invoked by an event and returns a response. Event sources can be events from [aws.S3](../devlog/aws.S3.md), [AWS DynamoDB](../devlog/AWS%20DynamoDB.md), [AWS API Gateway](../devlog/AWS%20API%20Gateway.md), [AWS SES](../devlog/AWS%20SES.md), based on these events we can many things.   
   
   
- The Lambda function (Code and Deployment package) is a single file.   
- Memory Size Specification.   
- Execution Timeout (15 minutes)   
- IAM Role(The Execution Role)   
- Event Source Mapping   
   
You are charged for when the Lambda function is invoked or how long it runs.   
   
If your functions are running for longer than 15 minutes, you might want to consider step functions. Run multiple functions in parallel.   
   
   
## Versions and Aliases   
   
You can publish one or more versions of your Lambda functions. Each Lambda function has a unique ARN. Once published it cannot be changed. Latest version of the function is tagged as **$Latest** (which happens to be default version).   
   
An Alias is a pointer to a specific Lambda function version. Each Alias has a unique ARN and unique Lambda functions they can be modified can be updated to point to different Lambda functions. They can be used for debugging and are ideal for rapid rollback deployments. Be careful when pointing multiple aliases to one version.   
   
## SAM Framework - Serverless Application Model   
   
It is an open source framework for building serverless applications. It provides shorthand syntax to expression functions, APIs, databases, event source mappings. We do this using [languages.YAML](../devlog/languages.YAML.md). It integrates with [aws.CloudFormation](../devlog/aws.CloudFormation.md). To use it we install [AWS SAM](../devlog/AWS%20SAM.md) Cli, it provides a Lambda like execution environment to locally build, test and debug your applications and prepare them for integration with CloudFormation.   
   
It provides a bridge between Lambda and CloudFormation. Ultimately, we can store our Lambda functions and execute them within CloudFormation(templates). It is basically a CloudFormation extension optimized for serverless applications. Using the **Transform function** we can include SAM code in our CF templates.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655655371/wiki/mhvxogw0tbatikroqohf.png)   
   
There is no charge for SAM. You’re only charged for the resources created.