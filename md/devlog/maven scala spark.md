---
created: 20211117152654744
desc: ''
id: c9r2joc5eh6lgdxcf1tl2xh
title: Maven Scala Spark
updated: 1653305106668
---
   
Topics::  [apache spark](../topics/apache%20spark.md)   
   
   
---   
   
Init a Scala project   
   
    mvn archetype:generate -DarchetypeGroupId=net.alchim31.maven -DarchetypeArtifactId=scala-archetype-simple -DdownloadSources=true   
   
ref: <[https://mvnrepository.com/artifact/net.alchim31.maven>](https://mvnrepository.com/artifact/net.alchim31.maven>)   
   
Add Spark dependency   
   
```
    <dependency>
      <groupId>org.apache.spark</groupId>
      <artifactId>spark-sql_2.12</artifactId>
      <version>3.1.1</version>
    </dependency>
```
   
   
   
- Make sure to select JDK 8   
- Make sure to select the right version of Scala (V 2.12.6?)   
- Make sure to "Generate Sources and Update Folders" by right clicking inside the `pom.xml` file and from the Maven options.   
- Run your `App.scala` to check if Scala has been installed properly   
- Write your program to check if Spark is working as expected   
   
<!-- end list -->   
   
    val data = spark.sparkContext.parallelize(Seq("Hello World", "This is some text", "Hello text"))   
    val map = data.flatMap(e => e.split(" ")).map(word => (word, 1))   
    val counts = map.reduceByKey(_ + _).repartition(1)   
   
    counts.saveAsTextFile("wordcount")   
   
    mvn clean package # to clean and package the .jar   
   
Using `spark-submit` to run your application   
   
`spark-submit --master "local[*]" --class com.zubayr.App target/spark-setup-1.0-SNAPSHOT.jar`