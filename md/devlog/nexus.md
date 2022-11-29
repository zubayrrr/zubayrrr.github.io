---
created: 1654593201127
desc: ''
id: vxce41k3oxe2gxzgenry4lj
title: Nexus
updated: 1657926610402
---
   
Nexus is an open-source [artifact repository](/not_created.md). It allows you to upload, download, store different built artifacts. It allows you to manage multiple repositories for different repository formats.   
   
Nexus is used as private or internal use only repository manager, where you can host your company internal own repositories. You can also create proxy repository (fetching from Maven and keeping it Nexus to centralize/consolidate)   
   
   
- You can integrate it with [LDAP](../devlog/ldap.md).   
- Flexible and powerful REST API end-point for integration with other tools.   
- Backup and restore.   
- Multi-format support (different artifact types - zip, tar, jar, war etc).   
- Metadata tagging (labelling and tagging artifacts).   
- Cleanup policies.   
- Search.   
- User token support for non-human users(system user authentication).   
   
You'll probably not use Nexus manually - it'll be part of your [build automation](../devlog/build%20automation.md) and [CICD pipeline](../devlog/CICD%20pipeline.md) cycle. It is meant to be integrated with tools like [jenkins](../devlog/jenkins.md) and other deployment tools.   
   
   
---   
   
   
- `Nexus` folder contains the runtime application of Nexus inside the `/bin`.   
- `Sonatype-work` folder contains your own config of Nexus and data.   
  - Different subdirectories will appear depending on your Nexus configuration, such as plugin directories.   
  - It also has a log file that has all the IP addresses that have accessed the Nexus application.   
  - It also has the log file for the Nexus application.   
  - It is where you upload your files and metadata.   
  - This folder is used to backup your Nexus application.   
- As a best practice, create a dedicated user to run this service with the permissions to access the above dirs.   
- Inside `Nexus/bin/nexus.rc` set `run_as_user=` to the newly created user.   
- To start Nexus `Nexus/bin/nexus start`.   
  - Use [netstat](../devlog/netstat.md) `-lnpt` to look for process ID and the port for external requests.   
  - Set inbound connections for that port on your server's firewall rules(TCP).   
- The Nexus UI will be available on `serverip:nexusport`.   
   
## Nexus UI   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654644255/wiki/xloscf79pdo22hnbly1d.png)   
   
   
- A default user(admin) is created along with password when you deploy Nexus.   
- Login and configure   
- Managing repositories   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1654644605/wiki/kijj1oitz8sgh1taphvp.png)   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1654644644/wiki/mudnethtl9ktehqp4ssr.png)   
    - By default some repositories are created.   
   
## Repository types   
   
   
- **Proxy** - linked to a remote repository such as Maven Central Repository. If you’re requesting a package, Nexus will first look locally to see if the requested package is available; if it isn’t, the request will be made to the remote repository and then stored on Nexus locally(and will act like a cache), it’ll also help you with bringing in proprietary/commercial packages that are not available externally.   
- **Hosted**   
- **Group** - grouping multiple repository end-points to a single repository end-point.   
   
## Create new repository   
   
   
- ![](https://res.cloudinary.com/zubayr/image/upload/v1654645683/wiki/ijv67etao7mokg2fklu0.png)   
   
## Publishing artifacts to Nexus repository.   
   
   
- Both Maven and Gradle have commands for pushing artifacts to remote repositories.   
- Maven and [Gradle](../devlog/Gradle.md) needs Nexus repo URL and credentials.   
- Nexus users are needed with permissions to upload.   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1654646661/wiki/z7pdilioj7ermzvy2jz0.png)   
  - Create role for the newly created users   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1654646774/wiki/cyzetrxf13ts8xzfwhfb.png)   
   
## Configuring Gradle for publishing to Nexus   
   
An example `build.gradle` will look something like this:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654647349/wiki/oycxy56ehtdfouhrk1xt.png)   
   
All that’s left is building `./gradlew build` and then `./gradlew publish`.
   
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
   
   
## Nexus API   
   
   
- It can be used to query your Nexus repo for different information.   
  - Which components, repositories, versions are available.   
- This information is needed for your [CICD pipeline](../devlog/CICD%20pipeline.md), to progmatically set the name, version of the artifact to be deployed.   
- Nexus API's REST endpoint can be used with tools like [curl](/not_created.md), [wget](../devlog/wget.md) to execute an http request.   
- A Nexus user is created with certain permissions and the user's credentials are used to make queries.   
   
   
- Making a request using curl to get repositories   
  - `curl -u user:pw -X GET 'http://ip-address:port/serivce/rest/v1/repositories'`   
  - It will return data in JSON format.   
- Making a request using curl to list all the components inside a repo   
  - `curl -u user:pw -X GET 'http://ip-address:port/serivce/rest/v1/components?repository=repo-name'`   
- You can also query using component ID   
  - `curl -u user:pw -X GET 'http://ip-address:port/serivce/rest/v1/components/component-id'`   
   
## Blob Store   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654651381/wiki/pxxp2ggectz2acun57hh.png)   
   
   
- Nexus uses Blob Store as storage for it's components.   
- Blob store is what Nexus is using to manage the storage per repository for all of it's components.   
- A blob store is an internal storage mechanism for binary parts of artifacts.   
- It can be on a local FS or on a cloud based storage like [s3](/not_created.md)   
- Each blob store can be used by one or multiple repository groups.   
- On drive it can be found at `/Sonatype-work/nexus3/blobs`.   
- Type field = Storage backend   
  - It can be file system-based storage(default)   
  - S3 - cloud based storage(when Nexus Repository Manager is hosted on AWS)   
- State field = State of the blob store   
  - started - running as expected   
  - failed - configuration issue - failed to initialize   
- Blob count field = number of blobs currently stored(`/blobs/default/content`)   
- Total size   
- Available space   
- Creating new blob store   
   
   
  - ![](https://res.cloudinary.com/zubayr/image/upload/v1654651357/wiki/w1gk5ilsrqc78n85lyxf.png)   
   
   
- Once created it cannot be modified   
- Blob store used by a repository cannot be deleted   
- One repository cannot use multiple blob store   
   
## Components VS Assets   
   
A component is more abstract - like the entire application that was uploaded. It is a generic definition, the term components refers to any type/format of package that was uploaded to the repository(an artifact, a package, archive etc).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654651811/wiki/e9ox01rt7okk17e8fbye.png)   
   
Assets are individual files inside the application.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654651861/wiki/f69xhzetjfeca6kedqtz.png)   
   
## Cleanup policies   
   
It helps you define rules that will cleanup artifacts(components) from the repository(either if they’re too old or haven’t been used in a long time etc) to free up storage for new components.   
   
Create a new policy   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654652487/wiki/n07gfou0xjnhsmwpiiwd.png)   
   
Make sure to attach the policy to a repository.   
   
As soon as a cleanup policy is created, a task is also created that will schedule the execution of the policy.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654652738/wiki/nw1hx6vze1oelsftyk5l.png)   
   
Cleanup will only mark them(the components) for deletion. It is called a softdelete. To actually delete files from the disk, the blob store needs to be compacted(a task can be created).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1654652902/wiki/pyvyzxlmqg1dckmhfv65.png)   
   
You can also manually trigger the tasks.   
   
See also: [nexus as docker container](../devlog/Nexus%20as%20Docker%20container.md)