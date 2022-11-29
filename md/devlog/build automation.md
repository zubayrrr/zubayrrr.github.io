---
created: 1654366736028
desc: ''
id: qcaw5ht4vcnucydq104gh7v
title: Build Automation
updated: 1654758092310
---
   
Related::  [jenkins](../devlog/jenkins.md)   
   
   
---   
   
## Build Automation   
   
Build automation refers to the process of taking the source code and the other artifacts created by the developers. We’ll build this code depending on the language they’re using; we’ll compile or transpile the code to generate an executable or simply a docker image.   
   
Build automation is one of the processes in a [CICD pipeline](../devlog/CICD%20pipeline.md)   
   
There are many tools that can help us with build automation such as: [jenkins](../devlog/jenkins.md)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654367652/wiki/kvbyhogruh45cxytkvrx.png)   
   
An example pipeline would look something like:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654707436/wiki/yu0yqhx2kwkjwdbg7ieg.png)   
   
## What do build and package manager tools do?   
   
They help with:   
   
   
- Compiling   
- Compressing   
- Transforming code from hundreds to a single file   
- Keep artifact in storage, in an artifact repository([nexus](../devlog/nexus.md)).   
- To deploy it multiple times(on different environments), make backups etc.   
   
   
---   
   
## Artifacts   
   
   
- Artifacts are apps built into a single, shareable, portable file.   
- Building Java applications produce a special artifact file such as a `.jar` or a `.war`.   
- Apps built from other programming languages may result in different artifact files such as a zip or a tarball.   
   
See also: [Artifact Repository](../devlog/Artifact%20Repository.md)   
   
## Building Java Applications   
   
   
- Install IntelliJ IDEA.   
- Install Java(or use IDEA to Download SDK).   
- Setup JDK, SDK (make sure Java executable is added to [path](/not_created.md) or `%PATH%`, respectively.)   
- Set `JAVA_HOME` as an [environment variable](../devlog/environment%20variable.md) (Maven prerequisite).   
- Use SCM to clone(`git clone`) your Java application's repository.   
   
   
- Build a [maven](../devlog/maven.md) project.   
   
   
  - Open source code of your Java application in IntelliJ IDEA.   
  - Wait for IDEA to index the source code.   
  - IDEA will automatically detect the `pom.xml` and resolve all the dependencies.   
  - Run the application(preview in the "Run" tab).   
  - Download [Maven](https://maven.apache.org) and add it's `/bin`'s path to `$PATH` or `%PATH%`.   
  - Use `mvn` commands and profit!   
  - After building, `.jar` or `.war` files can be found in the `./target` folder.   
   
   
- Build a [gradle](../devlog/Gradle.md) project.   
   
   
  - Open source code of your Java application in IntelliJ IDEA   
  - If it has a gradle wrapper(folder) inside the repo, you don't need to install gradle   
  - Make sure the JVM configured is compatible with gradle wrapper's version.(`JAVA_HOME`)   
  - Run the application to check if everything is working fine   
  - Build with `./gradlew build`   
  - After building, `.jar` or `.war` files can be found in the `./build` folder.   
   
To run a `.jar`: `java -jar name-of-the-app-SNAPSHOT.jar`   
   
## Managing Java dependencies   
   
   
- Build tools(Maven, Gradle, NPM) are required even for local development of the application.   
- Dependencies file is what keeps track of all the dependencies used in the application. Refer to `pom.xml` for a Maven project and `build.gradle` for a Gradle project.   
- All the dependencies for both kind of projects are fetched from [mvnrepository.com](https://mvnrepository.com), they're downloaded locally from the remote repository.   
   
## Building [languages.javascript](../devlog/languages.javascript.md) / [Nodejs](../devlog/Nodejs.md) project.   
   
   
- Install Node.js, run `npm` to check if everything is working correctly.   
- Alternatively to `npm` you can also use `yarn` to manage dependencies and to run build commands.   
- Use the build commands from `package.json` to build it.   
- Unlike Java applications, after building a JavaScript will result in `.zip` or `.tgz` file.   
- Both `npm` and `yarn` are **package managers not build tools**, they're used for managing dependencies not for transpiling JS code.   
- Use `npm pack` to pack.   
- The resulting zip or tar doesn't contain dependencies; only the application code.   
- To run the application, you first need to install the dependencies.   
- Unpack the zip/tar.   
- Run the app.   
   
   
- Package frontend JS code.   
  - Separate `package.json` for frontend and backend.   
  - or have a common `package.json` for both frontend and backend.   
  - React code needs to be transpiled since it uses `jsx` syntax.   
  - Compress and minify.   
- Build tools in the JavaScript world as also known as Bundlers.   
- Most popular bundler is [webpack](/not_created.md)   
- Webpack will transpile, minify, bundles, compresses(removes whitespaces etc).   
   
## Publishing build artifacts   
   
   
- All build tools have commands for publishing the artifacts to artifact repositories.   
- When you need the artifact, it can be [curl](/not_created.md)ed or [wget](../devlog/wget.md)ed when needed.   
   
## Enter [Docker](../devlog/docker.md)   
   
   
- With Docker in the picture, we don't really need multiple artifact repositories. We simply need a docker image repo.   
- Furthermore, we don't need to build and move different artifact types.   
- We also don't need to install dependencies on the server, we can simply execute commands inside the docker image.   
- You still need to build the apps and then create the docker images.   
- A single `dockerfile` can be used to make all the above steps seamless.   
   
**All of this is still part of the larger [CICD pipeline](/not_created.md)**   
   
See also: [nexus](../devlog/nexus.md)