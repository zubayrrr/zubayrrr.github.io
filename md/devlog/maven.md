---
created: '2021-11-12T00:00:00.000Z'
desc: ''
id: 482tfc3v73o3d4p8yi3b4z7
title: Maven
updated: 1660683241433
---
   
Topics::  [languages.java](../devlog/languages.java.md)   
   
   
---   
Convention over Configuration   
   
` mvn archetype:generate -DgroupId=com.zubayr -DartifactId=hellomaven -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`   
   
to generate a new maven project called "hellomaven"   
   
`mvn install` to build it   
   
`java -cp /target/hellomaven-1.0-SNAPSHOT.jar com.zubayr.App` to run the Java program.   
   
### Maven Plugins and Goals   
   
A maven plugin is a collection of goals.   
   
Goals such as `archetype:generate` `install:install`   
   
A goal can be a specific task, that we can run individually or can be part of a bigger build. (like compile, test, package)   
   
Goals can take in parameters such as   
   
`mvn archetype:generate -DgroundId=com.zubayr -DartifactId=hellomaven -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`   
   
We refer to a goal using `pluginId:goalId`   
   
By itself Maven doesn't really know create a project, compile, package etc   
   
It uses plugins to get the work done, every project gets a set of these plugins through the parent settings which can be overwritten using the `pom.xml` file   
   
### Phases and Goals   
   
For instance   
   
When you run `mvn install` you're asking maven to execute a lifecycle phase, maven has multiple lifecycle phases, such as:   
   
   
- `process-resources`   
- `compile`   
- `test`   
- `package` etc   
   
When you execute a maven package, it'll execute all the phases sequentially.   
   
Each lifecycle phase is associated with one or more goals, for example   
   
`process-resources` is associated with `resources:resources` (resources plugin, resources goal)   
   
We can have multiple goals associated with a phase but usually theres only one goal.   
   
The `compile` phase is associated with the `compiler:compiler`   
   
The `test` phase is associated with `surefire:test`   
   
You could also just say `mvn install surefire:test`, maven would then execute all the phases before `test` and then proceed with executing the `test` phase.   
   
Depending on the type of the pacakge the association might change, if you're building a standalone java project, the package phase will be assocaited with `jar:jar` and if its a web app it would be associated with `war:war` goal.   
   
## Maven Coordinates   
   
When we build a project, the plugins such as `jar` and `war` will look at the "Maven Coordinates" in the `pom.xml`   
   
Namely:   
   
   
- groundId   
- artifactId   
- version   
- packaging   
   
for the information about the project, these coordinates are represented internally as `groundId:artifactId:packaging:version` and it'll decicde where our project will be located in the Maven repository and name of the final output. (the `jar`, `war` that comes out of it)   
   
### groupId   
   
The groundId is similar to a Java package, the naming convention of a groundId is to reverse the URL of the company and if it has sub projects, such as a team, that can be included in the name.   
   
When the projects are placed into a Maven repostiry, it'll use these names and create folders with these names, very similar to packages.   
   
### artifactId   
   
It's kinda like a sub element of groupId and is used to name our project.   
   
### Version   
   
If you're continiously developing a project, initially it would have the word "SNAPSHOT" as per the naming convention. Once we release it, it'll have a solid version number associated with it.   
   
Example: \*`hellomaven-1.0-SNAPSHOT.jar` when its being developed \*`hellomaven-1.0.jar` once its released   
   
### Packaging   
   
The packaging element is not directly used in the naming/locating but indirectly packaging decides what type of project is being build.   
   
Using these coordinates we can also refer to this project as a dependency inside(`pom.xml`).   
   
the `junit` dependency info is used to pull the `junit` dependency from the Open source central repository of Maven.   
   
## Maven Repository   
   
Maven downloads it's packages, plugins, jars from a central location on the internet, it downloads it on the fly.   
   
default Maven location   
   
`http://repo.maven.apache.org/maven2/`   
   
Or when maven builds, it'll output the location where its hosting your repo   
   
The artifacts are stored under a certain folder structure, it is derived from the Maven Coordinates in the `pom.xml` of your project.   
   
It uses the `groupId` to create a repository, creates a subfolder using the `artifactId` and one more folder using the version number and the final output will be inside this version number folder.   
   
If you want certain repoistories that are not located on the Maven central repository, you'll have to use enterprise level repository will be used to get.   
   
## Configuring Maven for publishing to Nexus   
   
An example `pom.xml` will look something like this:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654647915/wiki/ps52q6penyp1thbar1pi.png)   
   
To configure user credentials for a repository on a Maven is in the `~/.m2/settings.xml` dir in your user’s `$HOME` dir.   
   
`settings.xml` will looking something like:   
   
```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
  ...
  <servers>
    <server>
      <id>server001</id>
      <username>my_login</username>
      <password>my_password</password>
      <privateKey>${user.home}/.ssh/id_dsa</privateKey>
      <passphrase>some_passphrase</passphrase>
      <filePermissions>664</filePermissions>
      <directoryPermissions>775</directoryPermissions>
      <configuration></configuration>
    </server>
  </servers>
  ...
</settings>
```
   
   
All that's left is `mvn package` and then `mvn deploy` to upload the `.jar` to the [Nexus](../devlog/nexus.md) repository.