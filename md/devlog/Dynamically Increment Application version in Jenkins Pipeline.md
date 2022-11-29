---
created: 1660683645204
desc: ''
id: 550xhuxruw489l6o5u36tyh
title: Dynamically Increment Application version in Jenkins Pipeline
updated: 1660687121913
---
   
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