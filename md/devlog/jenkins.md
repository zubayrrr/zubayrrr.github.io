---
created: 1653430069215
desc: ''
id: jqsu891tokqfup82wkq6j02
title: Jenkins
updated: 1664811273601
---
   
Jenkins is a continuous integration tool that allows continuous development, test and deployment of newly created code. Its a [build automation](../devlog/build%20automation.md) tool.   
   
   
- **Easy Installation** - Jenkins is a self contained java based program ready to run with packages for Windows, macOS and Linux operating systems.   
   
   
- **Easy Configuration** - Easy setup and configured via a web interface which includes error checks and built in help.   
   
   
- **Plugins** - Lots of plugins available in the Update Centre and integrates with many tools in the [CICD pipeline](/not_created.md) toolchain.   
   
   
- **Extensible** - In addition to the plugins, Jenkins can be extended by that plugin architecture which provides nearly infinite options for what it can be used for.   
   
   
- **Distributed** - Jenkins easily distributes work across multiple machines, helping to speed up builds, tests and deployments across multiple platforms.   
   
Jenkins is sort of acting as a middleman between many other tools. Such as [docker](../devlog/docker.md), build tools, repositories([nexus](../devlog/nexus.md)), deployment servers etc. Hence its needed to be integrated with all these tools, which is where it’s plugins come into the picture. For example:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654710271/wiki/slqynckdvxzbvnqpgz0c.png)   
   
Jenkins can be used to run tests, build artifacts, publish artifacts, deploy artifacts, send notifications etc.   
   
## How do you make Jenkins work?   
   
Jenkins User needs to have all the relevant permissions and tools available to it for it to be able to do it’s job.   
   
   
- Run tests   
  - Make build tools available to execute test commands. Tools like [npm](/not_created.md), [maven](../devlog/maven.md), [gradle](../devlog/Gradle.md)   
- Configure test environment   
  - Such as a test database   
- To build application   
  - Build tools or [docker](../devlog/docker.md)   
- To publish docker image   
  - You need to store credentials in Jenkins so it can access docker repository   
   
## Installing Jenkins   
   
### 1. Install Jenkins directly on the OS   
   
   
- Download package and install it   
- Create a new user for Jenkins on the server   
   
### 2. Run Jenkins as Docker Container   
   
   
- `docker run -p 8080:8080 -p 50000:50000 -d \ -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts`   
   
## Initialize Jenkins   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654758628/wiki/i7bxryvhzmeh9wcuhoz8.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654758825/wiki/kgoeo4x9vbx2bao7wjso.png)   
   
### Jenkins Roles   
   
1. Jenkins Administrator   
   
   
   - Operations or DevOps team   
   - Administers and manages Jenkins   
   - Sets up Jenkins cluster   
   - Installs plugins   
   - Backs up Jenkins data   
   - ![](https://res.cloudinary.com/zubayr/image/upload/v1654759517/wiki/lskadoodou7btzzjecwj.png)   
   
2. Jenkins User   
   
   - Developer or DevOps team   
   - Creating the actual jobs for run workflows   
   
## Installing build tools   
   
Depending on what application(programming language used) you’re building, you need to have different tools installed and configured on Jenkins.   
   
1. Install required plugin on Jenkins   
   
   
   - This approach can be limited to the input fields provided   
   - ![](https://res.cloudinary.com/zubayr/image/upload/v1654762016/wiki/yoxzochqrzziu0oxoisw.png)   
   - ![](https://res.cloudinary.com/zubayr/image/upload/v1654762087/wiki/war7fpncaxvvo0mooc8k.png)   
   - If a plugin is not available on “Global Tool Configuration” page it can be installed from “Manage Plugins” page   
   - ![](https://res.cloudinary.com/zubayr/image/upload/v1654762206/wiki/mjbfwr6itejojmx7hbs6.png)   
   
2. Install those tools directly on the server(where Jenkins is running)   
   
   - This approach is more flexible (scripting is easier)   
   - If your Jenkins is running as a [docker](../devlog/docker.md) container   
   - `docker exec -u 0 -it container-id bash`   
   - Install the tool inside the container based on the distro you’re using(`cat /etc/issue`)   
   
## Create a freestyle job   
   
Note: Freestyle jobs can be limiting because it can result in chaining freestyle jobs. The configuration is based on UI not scripting. It is not suitable for complex workflows. Plugins are limiting because of input field provided.   
Using freestyle jobs for multiple tasks can create chaining of freestyle jobs and its bad. They're for one singular step. You'll need multiple plugins managing them can be tedious.   
   
Select your type of job from “New Item” page   
Note: In prod, you’ll usually be dealing with a “Pipeline” job type   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654762490/wiki/okcheuvfts7fmczc1lzf.png)   
   
Configure your freestyle job   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654762596/wiki/y8a6hducx3kizheoeqov.png)   
   
On “Build” tab, write your shell commands to be executed.   
Note: You cannot use commands of plugins you’ve installed, only the programs you’ve installed directly on the server where Jenkins is running.   
**You can however “Invoke” the said plugin as a “Build step”**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654762838/wiki/t541ooixskhpr6xr6pbg.png)   
   
On Jenkins main view, you’ll find your list of jobs.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654762908/wiki/tevepvm7fv4ewkdfhxfj.png)   
   
You can also preview a build.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654762944/wiki/cpktacrn5nmocouewzza.png)   
   
## Configuring a [version control.git](../devlog/version%20control.git.md) repository   
   
Under “Source Code Management” tab   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654763672/wiki/wpg46yorlqlkp1isdzyc.png)   
   
Use “Jenkins Credentials Provider“ to add credentials   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654763750/wiki/nsidkaihilnbheepedbp.png)   
   
Whenever you run a job, Jenkins will checkout the code locally for latest commits and then it’ll run the job(test, build) against it.   
   
## Docker in Jenkins   
   
Making Docker available inside Jenkins   
   
Attaching a volume to Jenkins from the host. Currently our Jenkins is running on a server(where Docker commands are available), we can mount Docker runtime directory from the host into the container as a volume.   
   
Stop and start Jenkins docker container with additional volumes.   
   
   
- `docker stop container-id`   
- Move the old Jenkins config to the new container using the existing volume (`jenkins_home`)   
   
```
docker run -p 8080:8080 -p 50000:50000 -d \
-v jenkins_home:/var/jenkins_home \
-v /var/run/docker.sock:/var/run/docker.sock \
-v $(which docker):/usr/bin/docker jenkins/jenkins:lts
```
   
   
   
- `docker exec -it container-id bash`   
- Run `docker` to check if it’s available   
- However, you’ll not be allowed to pull any images, because the Jenkins service user doesn’t have permissions for the docker file(which was mounted from host)   
  - `ls -l /var/run/docker.sock`   
  - Add permissions for the Jenkins user by logging in as root user on the container   
  - `docker exec -u 0 -it container-id bash`   
  - `chmod 666 /var/run/docker.sock`   
  - Once done, you’ll be able to use docker commands inside the the Jenkins container while as the Jenkins service user.   
   
As part of our freestyle job, you can add shell commands to make an image out of the generated `.jar` and you can also push it to a docker repository(DockerHub).   
   
For pushing the image to the DockerHub repository, you will need to add credentials to Jenkins.   
   
And to use the credentials(insecure):   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654765785/wiki/wcul2oihla4vtmu0mido.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654765883/wiki/zwd5847ew0gf4mhffq5v.png)   
   
Tag the image using the repository name.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654765934/wiki/oklywlv24wee6ytbcbvv.png)   
   
If you were using a private repository other than DockerHub, you’d have to specify repository host name as an additional parameter for the `docker login` command   
   
A more secure way of passing the password is using standard input   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654766232/wiki/ktmvbbujpr4c8hj0h9on.png)   
   
## Push Docker image to [nexus](../devlog/nexus.md) repository   
   
   
- Before you can do this, you’ll need to register the Nexus repository’s IP and port explicitly by running `vim /etc/docker/daemon.conf` on the Nexus host.   
   
```json
{
  "insecure-registries": ["nexus-docker-repo-ip-address:port"]
}
```
   
   
   
- Restart docker `systemctl restart docker   
- Start Jenkins container   
- Add the permissions for the Jenkins user to use docker commands(scroll up to “Docker in Jenkins”)   
- Create credentials for Nexus Docker repository   
- Putting it all together will look something like   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654768504/wiki/yxpknd7sgvmkbysemwjj.png)   
   
Notice the Nexus [ip address](../devlog/ip%20address.md) and port substituted for repository location/name and for `docker login` the host is mentioned.   
   
## Pipeline jobs   
   
   
- Pipeline jobs are more suited for [CICD pipeline](/not_created.md), you can do scripting - pipeline as code.   
- To write a new script, go to the “Pipeline” tab after selecting “New item” → “Pipeline job”   
- - A pipeline job is recommended when you want to execute 2 tasks in parallel, or when you need user input if you want to programmatically use conditional statements in your pipeline script or even setting variables.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654774358/wiki/jvj6p0ekwiv96sauhtte.png)   
   
   
- Scripting is done in [groovy](/not_created.md)   
- Groovy sandbox means you can execute a limited no. of Groovy functions, for which you don’t need approval from a Jenkins admin.   
- Inline pipleline scripts are fine for small pipelines but best practice is having the pipeline script in a git repository.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654775265/wiki/fg0pusq07odw4l2etqbw.png)   
   
   
- The script should be written inside “Jenkinsfile” as the standard.   
   
## Pipeline Syntax   
   
   
- Scripted   
  - First syntax, allows usage of Groovy.   
  - Advanced scripting capabilities, high flexibility.   
  - Difficult to start.   
- Declarative   
  - Was added recently, make it easier to get started   
  - Predefined structure   
- Required fields (for declarative )   
  - “pipeline” must be top level   
  - “agent” where to execute(relevant for Jenkins cluster)   
  - “stages” where the “work” happens   
  - You can have multiple stages within which you will have “steps” which is where the actual commands go.   
- Required field (for scripted)   
  - You simply need “node”   
   
An example script after running will look something like   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654776281/wiki/nawyrptgirflydj5n0ij.png)   
   
## Jenkinsfile Syntax   
   
`#!/usr/bin/env groovy` is at the top of the file to let your editor know that you're working with a Groovy script.   
Whenever there is a variable inside a string, it has to use double quotes `""`.   
   
### `post` attribute   
   
Executes some logic after all the stages have been executed. It can have conditions with keywords like, `always` that will run regardless of the outcome of the stages. `success` will only run if all the stages have succeeded. `failure` will only run if any of the stages have failed. It basically defines build status or build state changes.   
   
```groovy
post {
  always {
    echo "This will always run"
  }
  success {
    echo "This will only run if all the stages have succeeded"
  }
  failure {
    echo "This will only run if any of the stages have failed"
  }
}
```
   
   
In Jenkinsfile, you can define conditionals for each stage.   
   
```groovy
pipeline {
  agent any
  stages {
    stage('Stage 1') {
      when {
        expression {
          BRANCH_NAME == "dev" || BRANCH_NAME == "master"
        }
      }
      steps {
        echo "Will only run if branch is dev or master"
      }
    }
    stage('Stage 2') {
      steps {
        echo "Stage 2"
      }
    }
  }
}
```
   
   
### Environmental variables   
   
You can use environmental variables in your Jenkinsfile which Jenkins has provided out of the box such as `BRANCH_NAME`. To find the list of available environmental variables, you can see `/env-vars.html`.   
   
You can define your own environmental variables in Jenkinsfile. They will be available for all the stages.   
   
```groovy
pipeline {
  agent any
  environment {
    NEW_VERSION = "1.0.0"
  }

  stages {
    stage('Build') {
      steps {
        echo "Building new version: ${NEW_VERSION}"
      }
    }
  }
}
```
   
   
Using credentials in Jenkinsfile. You will first have to define them in Jenkins GUI and then bind them to the env variable. For which you'll need "Credentials Binding" plugin.   
   
```groovy
pipeline {
  agent any
  environment {
    SERVER_CREDENTIALS = credentials('server-credentials')
  }

  stages {
    stage('Deploy') {
      steps {
        sh "${SERVER_CREDENTIALS}"
      }
    }
  }

  stages {
    stage('Deploy') {
      steps {
        echo "deploying the application"
        withCredentials([
          usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
        ]) {
          sh "echo ${USER} ${PWD}"
        }
        }
      }
    }
}
```
   
   
If you need the credentials only for one stage you can use a wrapper and define it inside the stage.   
   
### `tools` attribute   
   
Basically provides you build tools for your pipeline to build you project. It has to be preconfigured in Jenkins.   
   
```groovy
pipeline {
  agent any
  tools {
    maven 'Maven'
  }

  stages {
    stage('Build') {
      steps {
        echo "Building..."
        sh 'mvn install'
      }
    }
  }
}
```
   
   
### `parameters` attribute   
   
To parameterize your build.   
   
Type of parameters:   
   
   
- string (name, defaultvalue, description)   
- choice (name, choice, description)   
- booleanParam (name, defaultvalue, description)   
   
```groovy
pipeline {
  agent any
  parameters {
   // string(name: 'VERSION', defaultValue: '', description: 'Version to be deployed on production')
    choices(name: 'VERSION', choice: ['1.1.0', '1.2.0'], description: 'Version to be deployed on production')
    booleanParam(name: 'executeTests', defaultValue: true, description: '')
  }

  stages {
    stage('test') {
      when {
        expression{
          params.executeTests
        }
      }
      steps {
        echo "testing..."
      }
    }

    stage('Deploy') {
      steps {
          echo "Deploying application...."
          echo "Version number: ${params.VERSION}"
      }
    }
  }
}
```
   
   
Next time you run the job, it'll pull the latest changes from the Jenkinsfile and you'll be able to "Build with Parameters".   
   
You can use external scripts inside your groovy script. You can also write groovy code inside `script` attribute in your `steps`.   
   
```groovy
// groovy script
def build() {
  echo "building application"
}

def test() {
  echo "testing application"
}

def deploy() {
  echo "deploying application"
}

return this
```
   
   
```groovy
def gv
// making gv global
pipeline {
  agent any
  stages {
    stage('init') {
      steps {
        script {
          gv = load "external-script.groovy"
        }
      }
    }
  }

  stage ('build') {
    steps {
      script {
        gv.build()
      }
    }
  }

  stage ('test') {
    steps {
      script {
        gv.test()
      }
    }
  }

  stage ('deploy') {
    steps {
      script {
        gv.deploy()
      }
    }
  }
}
```
   
   
All environment variables from Jenkinsfile are available in the groovy script.   
   
### Input Parameters in Jenkinsfile   
   
User can input values for the parameters while running the job.   
   
```groovy
pipeline {
  agent any
  stages{
    stage('Deploy') {
      input {
        message: "Select the environment to deploy to"
        ok "Done"
        parameters {
            choices(name: 'ENV', choice: ['dev', 'staging', 'production'], description: 'Version to be deployed on production')
            // this is a scoped parameter, it is not global
            // you can also use script block but the syntax for input differs
        }
      }
      steps {
        echo "Deploying application...."
        echo "Deploying to ${ENV}"
        script {
          env.ENV = input message: "Select environment to deploy to", ok: "Done", parameters: [choices(name: 'ENV', choice: ['dev', 'staging', 'production'], description: 'Version to be deployed on production')]
        }
      }
    }
  }
}
```
   
   
### Multibranch Pipeline   
   
Single branch pipeline would look something like:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654854298/wiki/nsj9vutzvbdblniztxus.png)   
   
Typically, you’ll run tests on all the branches but you’d execute deployment only on Master branch. Other branches are merged into the Master branch and then the build, deploy jobs are triggered.   
   
Why do you need pipelines for all the branches? So that we can run tests to see everything is working properly on non-Master branches before merge.   
We also need different behaviour based on branch. For example: “If branch is master, run test, build and deploy” and “if branch isn’t master, run test and build skip deploy” etc.   
   
Pipelines need to be created dynamically in a Multibranch Pipeline.   
   
Select “Multibranch Pipeline” from the “New Item” page   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654854883/wiki/qbxeuoaytkq6wprkwais.png)   
   
Here, we can use regular expression to filter what branches to include. In this jobs, we’re choosing all the branches on the given repository. The rest of the build configuration will be made in the Jenkinsfile.   
   
## Jenkins credentials   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654858019/wiki/s6tnlznggh5akynpvajl.png)   
   
The credentials feature is thanks to a plugin. There are different credentials plugins that add more options(kinds of credentials).   
   
There are three scopes for credentials, System and Global credentials can be added on “Manage Credentials” view and Project specific credentials can be added from inside the job. System wide credentials will not be accessible inside the project.   
   
## Jenkins Shared Library   
   
Lets say we're working with a lot of micro services that contribute to one whole application. In Jenkins we'd use multi branch pipelines for each of that microservice. We'd build each of the microservice as a separate application; meaning you'd have multiple projects with multiple Jenkinsfiles for building those pipelines. Most of the logic in the Jenkinsfile would be same for all the applications in this case. Building `.jar`, building Docker images, pushing to Nexus repository...all these steps will be same for all the applications. To keep this aligned with DRY and to make this process efficient we use **Jenkins Shared Library**.   
   
   
- It is an extension to Pipelines.   
- It is it's own repository written in Groovy(just like Jenkinsfile).   
- We can write all the logic that is going to be shared across many different applications in a Shared Library and reference that logic in the Jenkinsfile in each project. (Basically, function calls in the Jenkinsfile).   
   
   
- It can also be used with different projects(with different teams).   
- If not all the steps are same in the Jenkinsfile across those different projects, whatever logic is common among those projects can be referenced from Shared Library instead of repeating the logic across multiple Jenkinsfile. E.g.   
  - Company wide Nexus repository.   
  - Company wide slack channel.   
   
### Create a Shared Library   
   
1. Init a git repository.   
2. Create a Groovy project in Maven and write the functions.   
3. Make the Shared Library available throughout Jenkins/or specific pipeline.   
4. Use the Shared Library in Jenkinsfile to extend the Pipeline.   
   
### Structure of Shared Library   
   
   
- Create a Groovy project in Maven.   
- Main folder `vars` contains all the functions that we're going to call from a Jenkinsfile.   
- Each function/execution step will be in its own Groovy script(inside `vars`).   
- `src` folder contains helper logic(utility code etc).   
- `resources` folder is where you'll keep your non-Groovy code(SQL scripts, external libraries, Powershell scripts, JSON files etc).   
   
```groovy
#!/usr/bin/env groovy

// vars/buildJar.groovy; functions(execution steps) are referenced by their filename

def call(){
  // here is where the logic goes
  echo "Building the application"
  sh "mvn package"
}

```
   
   
   
- Commit and push the code the git repository.   
- Make shared library available globally.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1658158197/wiki/h0ffz078kfggwfsddytc.png)   
   
Default version can either be a branch name, a commit hash or a tag. Having a fixed version is a good idea(to avoid breaking changes stopping a pipeline).   
   
   
- To use Shared Library in your Jenkinsfile:   
  - You'll need to import the Library in your Jenkinsfile.   
  - `@Library("jenkins-shared-library")_` you'll need to add an underscore at the end of the `@Library` call if you don't have any variable/function definitions/calls and have `pipeline{}` directly after.   
   
```groovy
#!/usr/bin/env groovy
@Library("jenkins-shared-library") // defined in Global Pipeline Libraries

def gv

pipeline{
  agent any
  tools{
    maven 'Maven'
  }
  stages{
    stage("init")
    ...
    stage("build jar"){
      steps{
        script{
          buildJar()
        }
      }
    }
    stage("build images"){
      steps{
        script{
          buildImage()
        }
      }
    }
  }
}
```
   
   
   
- Commit/push the changes to remote repo of the Jenkinsfile.   
   
### Passing Parameters to Methods   
   
```groovy
#!/usr/bin/env groovy

def call(String imageName){
  sh "docker build -t $imageName ."
  sh "docker push $imageName"
}
```
   
   
We can access global variables. We've all the environmental variables available in the Jenkinsfile also available in the Shared Library.   
   
**To extract logic into Groovy classes**:   
   
We can add a function's logic to a standalone file inside the `src` folder inside a class in a `package`.   
   
However, unlike the Shared Library, we do NOT have access to the global/environmental variables when we use separate classes. To make pipeline syntax available we use `script` keyword as parameter to the class's function.   
   
```groovy
// Docker.groovy
#!/usr/bin/env groovy

package com.example

class Docker implements Serializable{
  // `implements Serializable` to support saving the state of the execution if the pipeline is paused and then resumed.
  def script

  Docker(script){
    this.script = script
  }

  def buildDockerImage(String imageName) {
        script.echo "building the docker image..."
        script.sh "docker build -t $imageName ."
    }

    def dockerLogin() {
        script.withCredentials([script.usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
            script.sh "echo $script.PASS | docker login -u $script.USER --password-stdin"
        }
    }

    def dockerPush(String imageName) {
        script.sh "docker push $imageName"
    }

}
```
   
   
To call this function inside the `vars`'s groovy scripts   
   
**Note**: You can actually just call these class function directly to your Jenkinsfile instead of calling it in `vars` folder. But it is a best practice to call them in `vars` folder as an interface.   
   
These are just making calls to different function in a single class.   
   
```groovy
// buildImage.groovy
#!/usr/bin/env groovy

import com.example.Docker
def call (String imageName){
  // passing context from this function to the Docker class using `this` keyword
  return new Docker(this).buildDockerImage(imageName)
}
```
   
   
```groovy
// dockerLogin.groovy
#!/usr/bin/env groovy

import com.example.Docker

def call() {
    return new Docker(this).dockerLogin()
}
```
   
   
```groovy
// dockerPush.groovy
#!/usr/bin/env groovy

import com.example.Docker

def call(String imageName) {
    return new Docker(this).dockerPush(imageName)
}
```
   
   
You will call these function in your `Jenkinsfile`   
   
An alternative to having a Globally imported Shared Library, we can reference the library directly in the Jenkinsfile.   
   
Instead of using `@Library(jenkins-shared-library@master)...` use:   
   
```
library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
    [$class: 'GitSCMSource',
    remote: 'https://gitlab.com/user/shared-library.git',
    credentialsID: 'gitlab-credentials'
    ]
  )
```
   
   
## Webhooks   
   
You can trigger jobs either manually or automatically(preferable). An example of automatic trigger would be a git commit(any Git provider such as Gitlab or Github) triggering a job.   
   
Scheduling is another way of triggering build jobs. An example would be a job set up to be triggered after a certain time(maybe after running tests or a prior job that does some housekeeping etc).   
   
   
## Let's configure an automatic trigger of a Jenkins Job on a [version control.git](../devlog/version%20control.git.md) push.   
   
1. From "Manage Plugins" page install `Gitlab` for build triggers.   
2. From "Manage Jenkins" page -> "Configure System", find “Gitlab” section   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660674209/wiki/xdqlghfvcdwvf37ncrwe.png)   
   
3. Configure a Gitlab Connection   
   
   - Use Gitlab API Token(Personal Access Token)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660674456/wiki/oa8vjoyc8gfntpit0k0w.png)   
   
4.  A GitLab connection will now appear on your pipelines’ config page and the option for building on a push to GitLab repository   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660674626/wiki/sp0aoficzpvmpvq4rozm.png)   
   
The same options are available once GitLab connection is added on a freestyle job as well.   
   
5. Go to Gitlab(`repository-name/settings/integrations`) to find “Jenkins CI” to configure Gitlab to send a notification to Jenkins whenever a push is made.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660675011/wiki/fqvrsg30mjmgur8ubtb3.png)   
   
6. Save settings and Test settings   
   
   
---   
   
## Let’s configure automatic triggering of Jenkins job on a multibranch pipeline.   
   
The steps done for a regular pipeline cannot be applied to multibranch pipeline (Gitlab connection and options will appear but they’ll be in read-only mode).   
   
1. From Plugin Manager install “Multibranch Scan Webhook Trigger”.   
2. Go to config page on your multibranch  pipeline.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660675679/wiki/mwdw8cjo7z9o8vdqaz9u.png)   
   
   
3. Enable “Scan by webhook”    
4. Add a Trigger Token name(can be anything)   
5. Go to Gitlab(`repository/hooks`) webhooks   
6. Configure Gitlab to send a notification on a specific URL (Jenkins URL)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660675712/wiki/bom1cka6abihnilouuly.png)   
   
7. Add webhook once done configuring.
   
   
   
---   
   
## Dynamically Increment Application version in Jenkins Pipeline   
   
Generally speaking, all applications have a version and each build tool or package manager keeps track of this version in it's package/application build file. Example: `build.gradle`, `package.json`,`pom.xml`.   
   
Versioning is defined by the developer(or the team), of course there are best practices, standards around how to version. Versioning essentially keeps track of releases.   
   
The most common way of releasing/versioning schema is:   
   
**3 parts**. Example: `4.2.1`   
   
   
- 1st part tells the **Major Version**   
  - Contains big changes, breaking changes, often not backwards compatible.   
- 2nd part tells the **Minor Version**   
  - New changes/features, mostly backwards compatible.   
- 3rd part informs a **Patch**   
  - Minor changes, bug fixes etc.   
   
**-suffix** such as `1.0.1-SNAPSHOT` basically provides additional information(such as developmental/experimental releases). There are different suffixes in different teams; such as `RC` `2.3.5-RELEASE` or release candidate etc.   
   
There are different ways of versioning such as a **2 parts** schema etc.   
   
   
- The developers need to increment the version on each new release with respect to the kind of change/release.   
- This incrementing in most cases should be automated.   
- Each new version should be automatically be incremented in the build pipeline before release.   
   
See also: [semver](../devlog/semver.md)   
   
**Usually, build tools are able to take care of automating versioning.**   
   
For [Maven](../devlog/maven.md):   
   
   
- You can use a Maven plugin/command, example:   
   
`mvn build-helper:parse-version versions:set -DnewVersion=\${parsedVersion.majorVersion}.\${parsedVersion.minorVersion}.\${parsedVersion.nextIncrementalVersion} versions:commit`   
   
   
- The `parse-version` command/goal(of the plugin) automatically calculates the next version using variables.   
- It'll remove the old `pom.xml` and add a new with the requested changes(version bump).   
- See [Build Helper Maven Plugin](https://www.mojohaus.org/build-helper-maven-plugin/parse-version-mojo.html) for more information.   
   
It works similarly across the different package manager, build tools. There are other ways of doing it even on Maven using different plugins.   
   
**To integrate this process in a build pipeline:**   
   
   
## .jar Version   
   
In your `Jenkinsfile` add a stage for version increment before `mvn package` builds the application so that the `.jar` is produced with the correct version.   
   
```groovy
stage("increment version"){
  steps{
    script{
      echo "incrementing app version..."
      sh 'mvn build-helper:parse-version versions:set \
        -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
        versions:commit'
      def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
      def version = matcher[0][1]
      env.IMAGE_NAME = "$version-$BUILD_NUMBER" //$BUILD_NUMBER suffix is an env variable that jenkins makes available in our pipeline job. Every build has a number.
      // some developers use git commit has as a suffix too
    }
  }
}
```
   
   
## Docker Image Version   
   
If a new [docker](../devlog/docker.md) image is also built as part of your pipeline, you'd also want to bump it's version as well. Add another stage to accomplish this. Usually, the application version is used for the Docker Image version as well. The variable reads from the `pom.xml`   
   
Use the env variable created above when running `docker build` and `docker push`.   
Example: `docker build -t username/app-name:${IMAGE_VERSION} .`   
   
## Replace new version in Dockerfile   
   
Make the version defined in Dockerfile dynamic using [regular expression](../devlog/regular%20expression.md) and use `CMD` instead of `ENTRYPOINT`   
   
```dockerfile
...
COPY ./target/app-name-*.jar /usr/app/
WORKDIR /usr/app

CMD java -jar app-name-*.jar`
```
   
   
Alternatively, you can pass a parameter as a version value variable and use that etc.   
   
Note: **Don't forget to delete the older versions from your working directory using `mvn clean package`** in your Jenkinsfile build command. Don't use just `mvn package`.
   
   
   
Update the version bump of the `pom.xml` to the remote repository.   
   
Add another stage:   
   
```groovy
stage("commit version update") {
  steps {
    script {
      withCredentials([usernamePassword(credentialsId: 'gitlab-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
        sh 'git config --global user.email "jenkins@example.com"'
        sh 'git config --global user.name "jenkins"'
        sh 'git status'
        sh 'git branch'
        sh 'git config -l'
        sh "git remote set-url origin https://${USER}:${PASS}@gitlab.com/user/repo.git"
        sh 'git add .'
        sh 'git commit -m "version bump"'
        sh 'git push origin HEAD:jenkins-job'
      }
    }
  }
}
```
   
   
## Ignore Jenkins commit for Jenkins pipeline trigger   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660729401/wiki/uxjn1qhpaykw3kdin9hj.png)   
   
To avoid this:    
   
We need to detect that the commit was made by Jenkins user and not the developers and ignore the trigger for that commit.   
   
We can do this by installing “Ignore Committer Strategy” plugin.   
   
Once installed, “Build strategies” option will appear in the config of the pipeline.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660733313/wiki/rwkgbpplihk09sije8eb.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660733332/wiki/wognrezymwta43kq6dls.png)
   
   
## Source code   
   
   
- [zubayrrr / jenkins-shared-library · GitLab](https://gitlab.com/zubayrrr/jenkins-shared-library)   
   
## Look into   
   
   
- [Jenkins Node Configuration | Slave Concept & Architecture](https://www.soais.com/configure-jenkins-master-and-slave-nodes/)   
- [CloudBees Documentation](https://docs.cloudbees.com/)