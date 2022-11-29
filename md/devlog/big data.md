---
created: 20211109142548908
desc: ''
id: s5t9uscswvpo3p6gebui1ea
title: Big Data
updated: 1653318643709
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
Big Data is a term for collections of data sets so large and complex that it becomes difficult to process them using in-hand database management tools or traditional data processing applications.   
   
### 5 Vs of Big Data   
   
   
- Volume - Storing and processing huge data sets   
- Variety - Storing and processing different types of data   
- Velocity - The speed at which data is being generated   
- Value - Finding meaning out of data, making sense of data   
- Veracity - Uncertainty and inconsistencies in the data   
   
### Use cases:   
   
   
- Web and E-tailing   
  - Recommendation Engines   
  - Ad Targeting   
  - Search Quality   
- Telecommunications   
  - Abuse and Click Fraud Detection   
  - Customer Churn Prevention   
  - Network Performance Optimization   
  - Calling Data Record(CDR) Analysis   
  - Analyzing Network to Predict Failure   
- Banks and Financial Services   
  - Modeling True Risk   
  - Threat Analysis   
  - Fraud Detection   
  - Trade Surveillance   
  - Credit Scoring and Analysis   
- Retail   
  - Point of Sales Transaction Analysis   
  - Customer Churn Analysis   
  - Sentiment Analysis   
- Government   
  - Fraud Detection and Cybersecurity   
  - Welfare Schemes   
  - Justice   
- Healthcare and Life Sciences   
  - Health Information Exchange   
  - Gene Sequencing   
  - Serialization   
  - Healthcare Service Quality Improvements   
  - Drug Safety   
  - See [PoweredBy](https://cwiki.apache.org/confluence/display/HADOOP2/poweredby) for companies that are these technologies for Big Data   
- Semi-structured data   
- Unstructured data   
- Structured data   
- Large amount of data cannot fit on a single machine that needs processing is processed using distributed machines.   
- A distributed process has access to the computational resources across a number of machines connected through a network.   
- After a certain point, it is easier to scale out to many lower [CPU](../devlog/cpu.md) machines, than to try to scale up to a single machine with a high CPU.   
- Distributed machines also have the advanteage of easily scaling, you can just add more machines.   
- They also include fault tolerance, if one machines fails, the whole network can still go on.   
   
### [hadoop](../devlog/hadoop.md)   
   
   
- Hadoop is a way to distribute very large files across multiple machines.   
- It uses the Hadoop Distributed File System [hdfs](../devlog/hdfs.md)   
- HDFS allows a user to work with large data sets   
- HDFS also duplicates blocks of data for fault tolerance   
- It also then uses [mapreduce](../devlog/mapreduce.md)   
- MapReduce allows computations on that data   
- You've a NameNode(Master) and that connects to multiple DataNode(s)(Slave)   
   
Hadoop really only comes with HDFS and MapReduce and all the other technologies are addons, developed separately by different individuals.   
   
Java is highly preferable for MR   
   
   
- Pig was invented by Yahoo, PigLatin is the language, it a scripting language that was brought about to replace SQL/Java in MR. Internally it runs on MR and converts the code to Java. Most stuff that can be done on Hive can be done on Pig.   
- Sqoop was invented by a group, to bring data from RDBMS to Hadoop you write code in MapReduce, to avoid this, they brought about sqoop, sqoop doesn't use a programming language but commands to bring in data to Hadoop. sqoop also allows you to send data back to RDBMS from Hadoop. Import and Export. Used for Datapipeline, sqoop internally runs on Java.   
- Oozie was invented by Yahoo, its like an XML file, its a scheduler, used for automating, scheduling jobs, like running queries on a specific time. Big Data tech stack may include non Big Data specific schedulers. It runs on Java internally.   
   
All of above technologies discussed are abstractions of MapReduce.   
   
Big Data tech stack don't only consist of Big Data tools/technologies, MySQL for example is not a Big Data specific tool/technologies.   
   
### [HBase](#HBase)   
   
Storage part, Database for Hadoop but NoSQL, invented by Facebook, HBase shell commands, works on top of Hadoop, all the modern databases are NoSQL database.   
It is different from Hive.   
   
### Mahoot   
   
Framework for Data Science   
   
### Flume   
   
Similar to sqoop, used in datapipelines, flume can retrieve data in realtime. Messaging queue. sqoop is only for RDBMS unlike Flume which can be used for a fetching data from many other sources.(like twitter). Flume only retrieves data to Hadoop but cannot send it back to any other targets, only incoming.   
   
There are other MQs such as Kafka, Scribe.   
   
Hadoop is a losely couple framework, you can swap out/in components like oozie and it would still work, unlike tightly coupled frameworks(like .NET frameworks)   
   
Integrations - Hadoop can be integrated well with Spark or any other Big Data frameworks.   
   
Hadoop can also be connected with non Big Data components like [MySQL](../devlog/mysql.md) or other RDBMSes.   
   
### [hdfs](../devlog/hdfs.md)   
   
   
- HDFS will use blocks of data, with a size of 128 MB by default.   
- Each of these blocks is replicated 3 times.   
- The blocks are distributed in a way to support fault tolerance.   
- Smaller blocks provide more parallelization during processing.   
- Multiple copies of a block prevents loss of data due to a failure of a node.   
   
### MapReduce   
   
   
- MapReduce is a way of splitting a computation task to a distributed set of files (such as HDFS).   
- It consists of a Job Tracker and multiple Task Trackers.   
- The Job Tracker sends code to run on the Task Trackers.   
- The Task Trackers allocate CPU and memory for the tasks and monitor the tasks on the worker nodes.   
   
### Spark   
   
   
- One of the latest and open source technologies built to quickly and easily handle Big Data.   
- It is a Framework for dealing with large data, distributing it and doing calculations across distributed network. It is written in Scala. Scala gets the Spark's latest features, Scala is written in Java so Java can also be used for Spark's lastest features.   
- Created at AMPLab at UC Berkeley, first released in Feb of 2013.   
- It is a flexible alternative to MapReduce. (doesn't necessarily replaces Hadoop but MapReduce)   
- Spark can use data stored in a variety of formats   
  - Cassandra   
  - AWS S3   
  - [hdfs](../devlog/hdfs.md) and more   
   
### [apache spark](../topics/apache%20spark.md) VS [mapreduce](../devlog/mapreduce.md)   
   
   
- MapReduce requires files to be stored in HDFS, Spark does not\!   
- Spark also can perform operations up to 100x faster than MapReduce.   
- It is not really Hadoop VS MapReduce, people sometime make it as such because MapReduce uses HDFS.   
- MapReduce writes most data to disk after each Map and Reduce operation.   
- Spark keeps most of the data in memory something like RAM after each Transformation. Spark can spill over to [HDD](../devlog/hdd.md) if you don't have enough [RAM](../devlog/ram.md).   
   
### Spark RDDs   
   
   
- At the core of Spark is the idea of a Resilient Distributed Dataset(RDD).   
- Resilient Distributed Dataset (RDD) has 4 main features:   
  - Distrbuted Collections of Data   
  - Fault-tolerant   
  - Parallel operation - ability to be partitioned   
  - Ability to use many data sources   
   
At the abstract level it looks like:   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.ewfeqm3kqzs.png)   
   
At physical level:   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.3f0c49iwkep.png)   
   
   
- [rdd](../devlog/rdd.md)s are immutable, lazily evaluated and cacheable   
- There are two types of Spark operations:   
  - Transformations   
  - Actions   
- Transformations are basically a recipe to follow.   
- Actions actually perform what the recipe says to do and returns something back.   
- This behavior carries over to the syntax when coding.   
- A lot of times you will write a method call off of a [DataFrame](../devlog/dataframe.md) you won't see anything as a result until you call the action.   
- This makes sense because with a large dataset, you don't want to calculate all the transformations until you are sure you want to perform them\!   
- When discussing Spark syntax you'll often see RDD versus DataFrame syntax show up.   
- With the release of Spark 2.0, Spark is moving towards a DataFrame based syntax, but keep in mind that the way files are being distributed can still be thought of as RDDs(it is still happening in RDD at the pyhsical level), it is just the typed out syntax that is changing.   
   
### Spark [DataFrame](../devlog/dataframe.md)s   
   
   
- Spark DataFrames are also now the standard way of using Spark's Machine Learning capabilities.   
- Spark DataFrame documentation is still pretty new and can be sparse, it can be found on [spark.apache.org](https://spark.apache.org/docs/latest/)   
   
### Python and Spark   
   
   
- Realistically Spark won't be running on a single machine, it will run on a cluster on a service, like [AWS](../devlog/aws.md).   
- These cluster services will pretty much always be a [linux](../topics/linux.md)) based system.   
   
   
---   
   
## Miscellaneous Notes   
   
### Scalable Cluster Computing   
   
Scalable Cluster Computing is a method of combining discrete computing resources(e.g servers) to increase the performance of a single application.   
   
Does not work for applications\! (i.e., not all applications "scale")   
   
### Of Servers, Nodes and Daemons   
   
#### Server/Node   
   
A Cluster is a collection of servers working together on one problem.   
   
   
- Servers come with cores, memory, storage and network   
- Servers can be called a "**NODE**" in a cluster of servers   
   
#### Daemon   
   
A daemon is a program that is constantly running and responding to requests (e.g., web server)   
   
   
- Servers can have one or multiple daemons running on them   
- Daemons can communicate with other daemons and form a network within and between servers   
- Each daemon can also be called a "**NODE**"   
   
### Scalable Behaviour   
   
of Scalable Systems:   
The ability to apply resources (servers, VM instances) to a problem as a means to increase performance(green line) over a single server(red line).   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.t6kfn1dy0om.png)   
   
But, initially performance may lag due to overhead(the setup of our infrastructure).