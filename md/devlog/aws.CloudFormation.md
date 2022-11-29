---
created: 1655629188766
desc: ''
id: 7zaax8a13r0jjnssx46u39a
title: CloudFormation
updated: 1661779716554
---
   
It is an [IaC](../devlog/IaC.md) service that encourages collaboration and utilizes version control and automation. It can use a single template or multiple templates to create an environment and it can interact with other tools such as [Puppet](../devlog/puppet.md). You create a stack from a template. These templates can be stored on [aws.S3](../devlog/aws.S3.md)   
   
CloudFormation creates instances and Puppet puts those instances in a specific state.   
   
**Updating stack examples:**   
   
   
- Changing the AMI of our instances.   
- Updating a [aws.CloudWatch](../devlog/aws.CloudWatch.md) alarm.   
- Updating [AWS Auto Scaling Group](../devlog/AWS%20Auto%20Scaling%20Group.md) groups   
   
**Updating stack steps:**   
   
   
- Update the template.   
- Update the stack with the new template.   
   
**Stack policies:**   
   
   
- Can be used to prevent resource updates   
  - JSON Documents.   
  - Similar to IAM and Bucket policies.   
   
**Rollbacks:**   
   
If a stack fails and it attempts to rollback, it may get stuck on a single resource and often the troubleshooting of that is to manually delete that resource and then the stack will roll-the-wholeway-back.   
   
**Rollback failure:**   
   
Rollbacks can fail, there are dependencies in a stack and there is a certain order in which the resources have to be deleted.   
   
   
- Nested Stacks: Dependencies between resources; a resource was modified outside of the template.   
   
**Update considerations:**   
   
   
- How will the update affect the resource?   
- Is the change mutable or immutable?   
   
## CloudFormation Template   
   
A CloudFormation template is a declaration of AWS resources that make up a stack. Resources are declared in a template.   
   
   
- Resource map to a stack.   
- Declare an object as name-value pair or a pairing of a name with a set of objects enclosed.   
- The resources object is the only required object in a template.   
   
**Template Skeleton**   
   
```json
{
  "AWSTemplateFormatVersion" : "version date",

  "Description" : "JSON string",

  "Metadata" : {
    template metadata
  },

  "Parameters" : {
    set of parameters
  },

  "Rules" : {
    set of rules
  },

  "Mappings" : {
    set of mappings
  },

  "Conditions" : {
    set of conditions
  },

  "Transform" : {
    set of transforms
  },

  "Resources" : {
    set of resources
  },

  "Outputs" : {
    set of outputs
  }
}
```
   
   
Maintain the integrity of templates using version control and drift detection. It is vital that a template stored in another Region matches the template it would be replacing. CloudFormation templates are a valuable disaster recovery tool. Storing templates in a second Region is a common disaster recovery practice.   
   
## CloudFormation Intrinsic Functions   
   
They're built in CloudFormation functions which allow you to dynamically assign values to properties at run time.   
Eg: A function to retrieve public IP Address of an EC2 instance **at runtime** in the same stack. It allows us to reuse our templates.   
   
### Key Intrinsic functions   
   
   
- [Fn::Base64](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-base64.html)   
- [Fn::Cidr](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-cidr.html)   
- [Condition functions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-conditions.html)   
- [Fn::FindInMap](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-findinmap.html)   
- [Fn::GetAtt](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-getatt.html)   
- [Fn::GetAZs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-getavailabilityzones.html)   
- [Fn::ImportValue](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-importvalue.html)   
- [Fn::Join](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-join.html)   
- [Fn::Select](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-select.html)   
- [Fn::Split](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-split.html)   
- [Fn::Sub](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-sub.html)   
- [Fn::Transform](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-transform.html)   
- [Ref](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html./intrinsic-function-reference-ref.html)   
   
**They can only be used in specific parts of our template:**   
   
   
- Resource properties   
- Outputs   
- Metadata attributes   
- Update policy attributes   
   
It can also be used to conditionally create stacks.   
   
## CloudFormation Wait Conditions and Creation Policies   
   
They pause the execution of a stack creation and wait for a number of success signals(for a specified time period) before continuing stack creation. If it timesout, the stack creation will fail.   
   
   
- Timing mechanism, ensuring stack resource creation with configuration actions that are external to the stack creation.   
- Wait on the provisioning of resources.   
- Wait for an RDS database to be configured.   
- Wait for NAT instance to be configured before private instances attempt to access the internet.   
- Hybrid environment - AWS resources with On-prem resources.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655820410/wiki/vburerhncybkmthmejtr.png)   
   
**Wait condition properties:**   
   
   
- Count: Number of signals that CloudFormation must receive before it continues the stack creation process.   
- Handle: A reference to the wait condition handle used to signal this wait condition.   
- Timeout: A length of time (in seconds) to wait for the number of signals that the count property specifies.   
   
**Creation policy:**   
   
Pauses the creation of a resource until a requisite number of success signals are received.   
   
A Wait Condition is itself a CloudFormation resource.   
   
Creation Policy is an attribute associated with the resources. An EC2 instance could have an attribute of Creation Policy.   
   
For EC2 and Auto Scaling, it is recommended to use a Creation Policy.   
   
**CloudFormation helper scripts:**   
   
They’re a set of [languages.python](../devlog/languages.python.md) scripts to install software and start services on EC2 instances. They’re called directly from CloudFormation template. They also work with resource metadata defined in the template.   
   
Eg: Like sending signals back to the stack, update instances etc.   
   
`cfn-init`   
   
Retrieves and interprets the resource metadata to install packages, create files and start services. (Eg: Running LAMPStack)   
   
`cfn-signal`   
   
A simple wraper to signal an AWS CloudFormation Wait Condition for synchronizing other resources in the stack when the application is ready. It is also used the same way with Creation Policy   
   
`cfn-hup`   
   
A daemon that checks for updates to metadata and executes custom hooks when changes are detected.   
   
`cfn-get-metadata`   
   
A wrapper script that retrieves either all metadata that is defined for a resource or path to a specific key or a subtree of the resource metadata.   
   
## Resources   
   
   
- [What Is AWS CloudFormation? Concepts, Templates, and EC2 Use Case [Updated]](https://www.simplilearn.com/tutorials/aws-tutorial/aws-cloudformation)   
- [Creating EC2 instance in AWS with CloudFormation - Octopus Deploy](https://octopus.com/blog/aws-cloudformation-ec2-examples)