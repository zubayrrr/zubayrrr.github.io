---
created: 1655274148123
desc: ''
id: ajojjq9tu40v2rnmzktfyeo
title: AWS CodeBuild
updated: 1655461451522
---
   
AWS CodeBuild is a fully managed continuous integration service/build service that provides the similar capability that [Jenkins](../devlog/jenkins.md) can offer you.   
   
   
- Compiles your code   
- Runs unit tests   
- Produces artifacts that are ready to be deployed   
- Eliminates the need for provision/management of your infrastructure(build servers)   
- Provides pre-packaged build environments   
- Allows you to build your own customized build environments   
- Scales automatically to meet your build requirements   
- Charged only for the build time, based on operations performed   
- Output artifacts are stored in a secure [aws.S3](../devlog/aws.S3.md) bucket   
- The next service you will need is [AWS CodeDeploy](../devlog/AWS%20CodeDeploy.md) to complete the [CICD pipeline](../devlog/CICD%20pipeline.md)   
   
## Build Project   
   
A build project includes information about how to run a build, where to get the source code from, which build environment to use, which build commands to run and where to store the build output.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655274942/wiki/wtcdnu1dd0et00ge2hoz.png)   
   
   
- Under build specifications, you can choose either to use a `buildspec.yml` file with your instructions or you can choose to input commands for your build.   
- And of course, the `buildspec.yml` file needs to be part of your source code.   
- After successfully building your source code, the artifacts can be found on the chosen [aws.S3](../devlog/aws.S3.md) bucket.   
- Under “Build triggers” tab, you can schedule builds.   
- You can also setup notifications using [AWS SNS](/not_created.md)   
- You can keep an eye on this whole process using [aws.CloudWatch](../devlog/aws.CloudWatch.md)   
   
You can setup [aws.CloudWatch](../devlog/aws.CloudWatch.md) events to monitor the [AWS CodeCommit](../devlog/AWS%20CodeCommit.md) repository so that whenever there is a successful merge, CloudWatch will trigger a build.   
   
You can automate it further to keep an eye on the logs.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655461536/wiki/s5r31bu4nzwwkayxsgox.png)   
   
## `buildspec` file   
   
   
 -  A buildspec file is a collection of build commands related settings in [languages.YAML](../devlog/languages.YAML.md) format, that CodeBuild uses to run builds.   
 - You can include a buildspec as part of the source code or you can define buildspec when you create a build project.   
 - It must be named `buildspec.yml` and is located at the root of the source code.   
   
```yaml
# buildspecstub.yaml
version: 0.2

run-as: Linux-user-name

env:
  shell: shell-tag
  variables:
    AWS_ACCESS_KEY: "value"
    AWS_SECRET_ACCESS_KEY: "value"
    AWS_DEFAULT_REGION: us-east-1
    key: "value"
  parameter-store:
    key: "value"
    key: "value"
  exported-variables:
    - variable
    - variable
  secrets-manager:
    key: secret-id:json-key:version-stage:version-id
  git-credential-helper: no | yes

proxy:
  upload-artifacts: no | yes
  logs: no | yes

batch:
  fast-fail: false | true
  # build-list:
  # build-matrix:
  # build-graph:
        
phases:
  install:
    run-as: Linux-user-name
    on-failure: ABORT | CONTINUE
    runtime-versions:
      runtime: version
      java:corretto11
    commands:
      - command
      - command
    finally:
      - command
      - command
  pre_build:
    run-as: Linux-user-name
    on-failure: ABORT | CONTINUE
    commands:
      - command
      - command
    finally:
      - command
      - command
  build:
    run-as: Linux-user-name
    on-failure: ABORT | CONTINUE
    commands:
      - command
      - command
    finally:
      - command
      - command
  post_build:
    run-as: Linux-user-name
    on-failure: ABORT | CONTINUE
    commands:
      - command
      - command
    finally:
      - command
      - command
reports:
  report-group-name-or-arn:
    files:
      - location
      - location
    base-directory: location
    discard-paths: no | yes
    file-format: report-format
artifacts:
  files:
    - location
    - location
  name: artifact-name
  discard-paths: no | yes
  base-directory: location
  exclude-paths: excluded paths
  enable-symlinks: no | yes
  s3-prefix: prefix
  secondary-artifacts:
    artifactIdentifier:
      files:
        - location
        - location
      name: secondary-artifact-name
      discard-paths: no | yes
      base-directory: location
    artifactIdentifier:
      files:
        - location
        - location
      discard-paths: no | yes
      base-directory: location
cache:
  paths:
    - path
    - path
```
   
   
— via [Build specification reference for CodeBuild - AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)****