---
created: 1664806173667
desc: ''
id: t6uuv3bq4tt0rv5c9xf7t9z
title: Flashcards
updated: 1664806233503
---
   
## What is Continuous Integration?   
   
A development practice where developers integrate code into a shared repository frequently. It can range from a couple of changes every day or a week to a couple of changes in one hour in larger scales.   
   
Each piece of code (change/patch) is verified, to make the change is safe to merge. Today, it's a common practice to test the change using an automated build that makes sure the code can be integrated. It can be one build which runs several tests in different levels (unit, functional, etc.) or several separate builds that all or some has to pass in order for the change to be merged into the repository.   
   
## What is Continuous Deployment?   
   
A development strategy used by developers to release software automatically into production where any code commit must pass through an automated testing phase. Only when this is successful is the release considered production worthy. This eliminates any human interaction and should be implemented only after production-ready pipelines have been set with real-time monitoring and reporting of deployed assets. If any issues are detected in production it should be easy to rollback to previous working state.   
   
For more info please read [here](https://www.atlassian.com/continuous-delivery/continuous-deployment)   
   
## Can you describe an example of a CI (and/or CD) process starting the moment a developer submitted a change/PR to a repository?   
   
There are many answers for such a question, as CI processes vary, depending on the technologies used and the type of the project to where the change was submitted.   
Such processes can include one or more of the following stages:   
   
   
- Compile   
- Build   
- Install   
- Configure   
- Update   
- Test   
   
An example of one possible answer:   
   
A developer submitted a pull request to a project. The PR (pull request) triggered two jobs (or one combined job). One job for running lint test on the change and the second job for building a package which includes the submitted change, and running multiple api/scenario tests using that package. Once all tests passed and the change was approved by a maintainer/core, it's merged/pushed to the repository. If some of the tests failed, the change will not be allowed to merged/pushed to the repository.   
   
A complete different answer or CI process, can describe how a developer pushes code to a repository, a workflow then triggered to build a container image and push it to the registry. Once in the registry, the k8s cluster is applied with the new changes.   
   
## What is Continuous Delivery?   
   
A development strategy used to frequently deliver code to QA and Ops for testing. This entails having a staging area that has production like features where changes can only be accepted for production after a manual review. Because of this human entanglement there is usually a time lag between release and review making it slower and error prone as compared to continuous deployment.   
   
For more info please read [here](https://www.atlassian.com/continuous-delivery/continuous-deployment)   
   
## What is difference between Continuous Delivery and Continuous Deployment?   
   
Both encapsulate the same process of deploying the changes which were compiled and/or tested in the CI pipelines.<br>   
The difference between the two is that Continuous Delivery isn't fully automated process as opposed to Continuous Deployment where every change that is tested in the process is eventually deployed to production. In continuous delivery someone is either approving the deployment process or the deployment process is based on constraints and conditions (like time constraint of deploying every week/month/...)   
   
## What CI/CD best practices are you familiar with? Or what do you consider as CI/CD best practice?   
   
   
- Commit and test often.   
- Testing/Staging environment should be a clone of production environment.   
- Clean up your environments (e.g. your CI/CD pipelines may create a lot of resources. They should also take care of cleaning up everything they create)   
- The CI/CD pipelines should provide the same results when executed locally or remotely   
- Treat CI/CD as another application in your organization. Not as a glue code.   
- On demand environments instead of pre-allocated resources for CI/CD purposes   
- Stages/Steps/Tasks of pipelines should be shared between applications or microservices (don't re-invent common tasks like "cloning a project")   
   
## You are given a pipeline and a pool with 3 workers: virtual machine, baremetal and a container. How will you decide on which one of them to run the pipeline?   
   
## Where do you store CI/CD pipelines? Why?   
   
There are multiple approaches as to where to store the CI/CD pipeline definitions:   
   
1. App Repository - store them in the same repository of the application they are building or testing (perhaps the most popular one)   
2. Central Repository - store all organization's/project's CI/CD pipelines in one separate repository (perhaps the best approach when multiple teams test the same set of projects and they end up having many pipelines)   
3. CI repo for every app repo - you separate CI related code from app code but you don't put everything in one place (perhaps the worst option due to the maintenance)   
4. The platform where the CI/CD pipelines are being executed (e.g. Kubernetes Cluster in case of Tekton/OpenShift Pipelines).   
   
## How do you perform plan capacity for your CI/CD resources? (e.g. servers, storage, etc.)   
   
## How would you structure/implement CD for an application which depends on several other applications?   
   
## How do you measure your CI/CD quality? Are there any metrics or KPIs you are using for measuring the quality?   
   
## What is Jenkins? What have you used it for?   
   
Jenkins is an open source automation tool written in Java with plugins built for Continuous Integration purpose. Jenkins is used to build and test your software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build. It also allows you to continuously deliver your software by integrating with a large number of testing and deployment technologies.   
   
Jenkins integrates development life-cycle processes of all kinds, including build, document, test, package, stage, deploy, static analysis and much more.   
   
## What are the advantages of Jenkins over its competitors? Can you compare it to one of the following systems?   
   
   
- Travis   
- Bamboo   
- Teamcity   
- CircleCI   
   
## What are the limitations or disadvantages of Jenkins?   
   
This might be considered to be an opinionated answer:   
   
   
- Old fashioned dashboards with not many options to customize it   
- Containers readiness (this has improved with Jenkins X)   
- By itself, it doesn't have many features. On the other hand, there many plugins created by the community to expand its abilities   
- Managing Jenkins and its pipelines as a code can be one hell of a nightmare   
   
## Explain the following:   
   
   
- Job   
- Build   
- Plugin   
- Node or Worker   
- Executor   
- Job is an automation definition = what and where to execute once the user clicks on "build"   
- Build is a running instance of a job. You can have one or more builds at any given point of time (unless limited by configuration)   
- A worker is the machine/instance on which the build is running. When a build starts, it "acquires" a worker out of a pool to run on it.   
- An executor is variable of the worker, defining how many builds can run on that worker in parallel. An executor value of 3 means, that 3 builds can run at any point on that executor (not necessarily of the same job. Any builds)   
   
## What plugins have you used in Jenkins?   
   
## Have you used Jenkins for CI or CD processes? Can you describe them?   
   
## What type of jobs are there? Which types have you used?   
   
## How did you report build results to users? What ways are there to report the results?   
   
You can report via:   
   
   
- Emails   
- Messaging apps   
- Dashboards   
   
Each has its own disadvantages and advantages. Emails for example, if sent too often, can be eventually disregarded or ignored.   
   
## You need to run unit tests every time a change submitted to a given project. Describe in details how your pipeline would look like and what will be executed in each stage   
   
The pipelines will have multiple stages:   
   
   
- Clone the project   
- Install test dependencies (for example, if I need tox package to run the tests, I will install it in this stage)   
- Run unit tests   
- (Optional) report results (For example an email to the users)   
- Archive the relevant logs/files   
   
## How to secure Jenkins?   
   
[Jenkins documentation](https://www.jenkins.io/doc/book/security/securing-jenkins/) provides some basic intro for securing your Jenkins server.   
   
## Describe how do you add new nodes (agents) to Jenkins   
   
You can describe the UI way to add new nodes but better to explain how to do in a way that scales like a script or using dynamic source for nodes like one of the existing clouds.   
   
## How to acquire multiple nodes for one specific build?   
   
## Whenever a build fails, you would like to notify the team owning the job regarding the failure and provide failure reason. How would you do that?   
   
## There are four teams in your organization. How to prioritize the builds of each team? So the jobs of team x will always run before team y for example   
   
## If you are managing a dozen of jobs, you can probably use the Jenkins UI. But how do you manage the creation and deletion of hundreds of jobs every week/month?   
   
## What are some of Jenkins limitations?   
   
   
- Testing cross-dependencies (changes from multiple projects together)   
- Starting builds from any stage (although Cloudbees implemented something called checkpoints)   
   
## What is the different between a scripted pipeline to declarative pipeline? Which type are you using?   
   
## How would you implement an option of a starting a build from a certain stage and not from the beginning?   
   
## Do you have experience with developing a Jenkins plugin? Can you describe this experience?   
   
## Have you written Jenkins scripts? If yes, what for and how they work?   
   
## What is a Workflow in GitHub Actions?   
   
A YAML file that defines the automation actions and instructions to execute upon a specific event.<br>   
The file is placed in the repository itself.   
   
A Workflow can be anything - running tests, compiling code, building packages, ...   
   
## What is a Runner in GitHub Actions?   
   
A workflow has to be executed somewhere. The environment where the workflow is executed is called Runner.<br>   
A Runner can be an on-premise host or GitHub hoste   
   
## What is a Job in GitHub Actions?   
   
A job is a series of steps which are executed on the same runner/environment.<br>   
A workflow must include at least one job.   
   
## What is an Action in GitHub Actions?   
   
An action is the smallest unit in a workflow. It includes the commands to execute as part of the job.   
   
## In GitHub Actions workflow, what the 'on' attribute/directive is used for?   
   
Specify upon which events the workflow will be triggered.<br>   
For example, you might configure the workflow to trigger every time a changed is pushed to the repository.   
   
## True or False? In Github Actions, jobs are executed in parallel by deafult   
   
True   
   
## How to create dependencies between jobs so one job runs after another?   
   
Using the "needs" attribute/directive.   
   
```
jobs:
  job1:
  job2:
    needs: job1
```
   
   
In the above example, job1 must complete successfully before job2 runs   
   
## How to add a Workflow to a repository?   
   
CLI:   
   
1. Create the directory `.github/workflows` in the repository   
2. Add a YAML file   
   
UI:   
   
1. In the repository page, click on "Actions"   
2. Choose workflow and click on "Set up this workflow"   
   
## In Zuul, What are the <code>check</code> pipelines?   
   
`check` pipeline are triggered when a patch is uploaded to a code review system (e.g. Gerrit).<br>   
   
## In Zuul, What are the <code>gate</code> pipelines?   
   
`gate` pipeline are triggered when a code reviewer approves the change in a code review system (e.g. Gerrit)   
   
## True or False? <code>gate</code> pipelines run after the <code>check</code> pipelines   
   
True. `check` pipeline run when the change is uploaded, while the `gate` pipelines run when the change is approved by a reviewer