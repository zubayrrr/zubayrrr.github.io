---
created: 20211115133856116
desc: ''
id: f2kecna72pmc7re3wh1ugk4
tags:
- topics
title: Apache Spark
updated: 1653318643716
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
### Context of Big Data   
   
Computing vs Data   
   
   
- CPUs are only incrementally faster   
- Data storage keeps getting better and cheaper   
- Gathering data kees getting easier and cheaper and more important   
   
Data needs to be distributed and processed in parallel   
   
Standard single-CPU software cannot scale up   
   
Thus Spark was born.   
   
### Motivation for Spark   
   
A 2009 UC Berkeley project Matei Zaharia el al   
   
   
- MapReduce was the king of large distributed computation   
- Inefficient for large applications and ML   
- Each step required another data pass, written as separate application   
   
Spark phase 1   
   
   
- A simple functional programming API   
- Optimize multi-step applications   
- In-memory computation and data-sharing aross nodes   
   
Spark phase 2   
   
   
- Interactive data science and ad-hoc computation   
- Spark shell and Spark SQL   
   
Spark phase 3   
   
   
- Same engine, new libraries   
- ML, Streaming, GraphX   
   
## Spark First Principles   
   
Spark is unified computing engine and libraries for distributed data processing at scale.   
   
It is an open source data processing engine(in-memory computing engine) to store and process data in real-time across various clusters of computers using simple programming constructs.   
   
Big data = data that cannot fit on a standard computer, you'll need a cluster of computers that can process that data.(and Spark was made for this specific task)   
   
   
- Spark supports a variety of data processing tasks   
  - data loading   
  - SQL queries   
  - machine learning   
  - streaming   
- Unified in the sense:   
  - consistent, composable APIs in multiple languages   
  - optimizations across different libraries   
- Computig engine in the sense that it is detached from data storage(where the data resides) and how the data is being fetched(I/O)   
- Libraries   
  - standard: Spark SQL, MLlib, Streaming, GraphX   
  - hundres of open-source third party libraries   
   
### [hadoop](../devlog/hadoop.md) vs Spark   
   
Hadoop   
   
   
- Processing data using [mapreduce](../devlog/mapreduce.md) in hadoop is slow.   
- Performs batch processing of data, intermittent data is written to [hdfs](../devlog/hdfs.md) and read back from [hdfs](../devlog/hdfs.md) which makes hadoop's MapReduce slow.   
- hadoop has more lines of code. Since it is written in Java, it takes more time to execute.   
- hadoop supports [Kerberos](/not_created.md) authentication, which is difficult to manage.   
   
Spark   
   
   
- Spark processes data 100 times faster than MapReduce as it is done in-memory (like [Tez](../devlog/tez.md)).   
- Performs both batch processing and real-time processing of data, most use cases are around real-time processing.   
- Spark hs fewer lines of code as it is implemented in [scala](../devlog/scala.md).   
- Spark supports authentication via a shared secret. It can also run on [yarn](../devlog/yarn.md) leveraging the capability of [Kerberos](/not_created.md).   
   
### Spark Features   
   
Fast processing   
   
   
- Spark contains [rdd](../devlog/rdd.md)s which saves time taken in reading and writing operations and hence, it runs almost ten to hundred times faster than hadoop.   
- In-memory computing - In Spark data is stored in the RAM, so it can access the data quickly and accelerate the speed of analytics.   
  - Caching is different from In-memory computing, caching is mainly to support "read ahead" mechanism, where you have your data preloaded so that it can benefit further queries.   
  - In-memory computing is more about lazy evaluation, data being loaded in memory only and only if a specific action is invoked.   
- Flexible - polyglot   
- Fault tolerance - Spark contains [rdd](../devlog/rdd.md)s (execution logic, temporary datasets which initially do not have any data loaded and data will only be loaded into RDDs when an execution is made) that are designed to handle the failure of any worker node in the cluster. Thus, it ensures that the loss of data reduces to zero.   
  - Distributed   
- Better analytics - Spark has a rich set of SQL queries, machine learning algorithms, complex analytics etc.   
   
### Spark Misconceptions   
   
Spark is not concerned with data sources   
   
Spark is not part of [hadoop](../devlog/hadoop.md), it interacts with Hadoop and HDFS well but it is it's own thing.   
   
## Components of Apache Spark   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.cct1xwxfey9.png)   
   
[Spark Core](../devlog/spark%20core.md)   
   
   
- Contains [rdd](../devlog/rdd.md)s; core engine that takes care of processing   
   
See also: [DAG](../devlog/dag.md)   
   
[Spark SQL](../devlog/spark%20sql.md)   
   
   
- For working with structured data or data that can be structurized.   
- Has internal features such as Dataframes, datasets used to process structued data in much faster way.   
   
[Spark Streaming](../devlog/spark%20streaming.md)   
   
   
- Allows you to create Spark Streaming applications which not only works on data that is being streamed/generated in but also transform the data and analyze it as it comes in.   
   
[Spark MLlib](../devlog/spark%20mllib.md)   
   
   
- For building machine learning algorithms, predictive analytics, perscriptive, descriptive, preemptive, recommendation systems.   
   
[GraphX](../devlog/graphx.md)   
   
   
- Data naturally has a network kind of flow, data that be represented with graphs(not really pie charts) but network related data, some kind of relationships, twitter, fb, linkedin etc.   
   
## Spark Architecture   
   
Apache Spark uses a master-slave(technically, although it can also run in standalone mode) architecture that consists of a driver, that runs on a master node and multiple executors which run across the worker nodes in the cluster.   
   
It can work with different clustering technologies such as Apache Mesos, [yarn](../devlog/yarn.md). It can also work as standalone.   
   
Master Node has a driver program; this driver program internally has SparkContext.   
   
The Spark code behaves as a driver program and creates a SparkContext, which is gateway to all the Spark functionalities.   
   
Driver program interacts with cluster manager(SparkContext, the entry point, takes the request to the cluster manager).   
   
Cluster manager in terms of YARN is the `ResourceManager`   
   
Spark application runs as independent set of processes on a cluster.   
   
The driver program and SparkContext takes care of the job execution within the cluster.   
   
A job is split into multiple tasks that are distributed over the worker node.   
   
When an [rdd](../devlog/rdd.md) is created in SparkContext, it can be distributed across various nodes.   
   
Worker nodes are slaves that run different tasks.   
   
   
---   
   
Spark Architecture is based on 2 important abstractions:   
   
### [rdd](../devlog/rdd.md)   
   
Resilient Distributed Datasets   
   
Spark Core is embedded with RDDs, an immutable fault-tolerant(like files in [hdfs](../devlog/hdfs.md)), distributed collection of objects that can be operated on in parallel.   
   
It where the data will be loaded(or existing for processing), it can exist for shorter amount of time.   
   
   
- RDDs are the fundamental units of data in Apache Spark that are split into partitions and can be executed on different nodes of a cluster. Implicit, lazy in nature, created whenever you use a method of SparkContext or when you do a transformation on an existing RDD or a dataset.   
- Each dataset in an RDD is divided into logical memory partitions that may be computed on different nodes of a cluster.   
- By default every RDD has 2 partitions, which can be customized while creating RDDs.   
- The more partitions you've the better the parallel processing.   
- RDDs are automatically split into partitions and can be executed upon different nodes by different taks in parallel, in-memory.   
   
There are mainly two operations that can be peformed on an RDD   
   
### Transformation   
   
   
- These are operations (such as map, filter, join, union) that are peformed on an RDD that yields as new RDD containing the result.   
- They return a pointer to a new RDD. The original RDD cannot be changed. Spark is "lazy" and nothing will be executed unless an action is invoked.   
- It isn't necessarily reproducing a new set of data or RDD, but is a new "state". Think of it as step(s) in a program telling Spark how to get new data and what to do with it.   
- **Resilience** is the ability to retrace steps from the beginning.   
   
### Actions   
   
   
- These are operations (reduce, first, count, collect, count, take save-as) that return a value after running a computation on an RDD.   
- They return values and force the transformations to actually take place.   
   
See also: [DAG](../devlog/dag.md)   
   
### [DAG](../devlog/dag.md)   
   
Directed Acyclic Graph   
   
Spark has a DAG scheduler in the background which is tracking the transformations and steps which is part of your applications.   
   
It is the scheduling layer of the Spark Architecture that implements stage-oriented scheduling and eliminates that hadoop [mapreduce](../devlog/mapreduce.md) multistage execution model.   
   
If you're processing data using Spark applications in a Spark platform(whether standalone or in a hadoop cluster), for every step you do as part of your application, it creates an [rdd](../devlog/rdd.md), it becomes part of your DAG. The DAG scheduler is already aware of what steps are involved in DAG hence it comes up with a plan for executing the all the steps within the DAG. <span class="underline">If only and only if an action is invoked.</span>   
   
Check <[https://data-flair.training/blogs/dag-in-apache-spark/>](https://data-flair.training/blogs/dag-in-apache-spark/>)   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.muzlc82nhqb.png)   
   
See also: [Spark Cluster Managers](../devlog/spark%20cluster%20managers.md)   
   
## Spark Data Slicing   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.4ylqh1r70re.png)   
   
in contrast with Slicing in [hadoop](../devlog/hadoop.md)   
   
Slicing in [hadoop](../devlog/hadoop.md) vs [Slicing in Spark](../devlog/slicing%20in%20spark.md)   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.83j55a3bdv5.png)   
   
   
---   
   
## [DataFrame](../devlog/dataframe.md)   
   
DataFrame is a distributed collection of data organized into named columns. ... DataFrames can be constructed from a wide array of sources such as: structured data files, tables in Hive, external databases, or existing RDDs.   
   
Created a SparkSession(it allows creating, reading and writing DataFrames)   
   
    val spark = SparkSession.builder()   
        .appName("My Application")   
        .config("spark.master", "local")   
        .getOrCreate()   
   
Reading a DataFrame from a file   
   
    var firstDF = spark.read()   
        .format("json")   
        .option("inferSchema", "true")   
        .load("path/to/file.json")   
   
Performing operations on a DataFrame   
   
    firstDF.show()   
    firstDF.printSchema()   
    firstDF.take(5)   
   
Rows = unstructured data; and the information about the structure of the data is applied to the DataFrame in the form of a Schema   
   
Schema = description of fields aka columns and their type   
   
Spark types, they spark at runtime rather than compile time.   
   
   
---   
   
### How DataFrames Work   
   
Distributed spreadsheets with rows and columns, like a table that is split between multiple nodes in a Spark cluster, the information each Spark node recieves is the schema of the DataFrame anda few of the rows that compose the DataFrame.   
   
Distributed collections of Rows conforming to a schema   
   
DataFrames are:   
   
   
- Immutable   
  - Can't be changed once created   
  - If you want to modify them you will have to create new DataFrames using transformations   
   
Schema = list describing the column names and types   
   
   
- Types are known to Spark when the DataFrame is being used, not at compile time(to make them available at compile time with Type safe Datasets)   
- Schema can hold arbitrary number of columns   
- All rows have the same structure   
- Rows do not have schema but they conform to the same structure   
   
<!-- end list -->   
   
    val carsSchema = StructType(Array(   
        StructField("Name", StringType),   
        StructField("HorsePower", IntegerType),   
        StructField("Acceleration", DoubleType)   
    ))   
   
### Need to be distributed   
   
These collections of rows need to be distributed, because either the data is too big for a single computer or it takes too long to process entier data on a single CPU.   
   
### Partitioning   
   
   
- Splits the data into files, distributed between nodes in the cluster   
- Impacts the processing parallelism   
- More partitions may mean more parallelism but if you have 1000 partitions (1000 small files that compose your DataFrame) and a single node to process them all, parallelism will still be one because you only have one node to process all that data.   
- Inversely, if you have 1 partition and many nodes in your Spark cluster, only one node will have access to that partition and the parallelism would still be one.   
   
### Transformations   
   
   
- Narrow = one input partition contributes to at most one output partition(e.g map), partitioning is not changed in a DataFrame.   
  - If you do a map, that would transform data row by row and so the partitioning is not changed, whereas   
- Wide = input partitions(one or more) create many output partitions, so the partitioning of the DataFrame is changed.   
  - If you do a sort, that will involve exchanging data between partitions in between nodes in the cluster.   
- These operations are known as Shuffle = data exchange between cluster nodes.   
  - Shuffling occurs in Wide transformations and its a massive performance topic, it can impact the time it takes for your jobs by orders of magnitude.   
   
### Computing DataFrames   
   
How DataFrames work at runtime   
   
Lazy evaluation   
   
   
- Spark mechanism to wait until the last moment to execute the DF transformations   
   
Planning   
   
   
- Spark compiles the DF transformations and dependencies into a graph before running any code, Spark will know before hand every single step that it will have to take including data exchanges between nodes before it actually starts loading or running any code.   
- Logical plan = DF dependency graph + narrow/wide transformations sequence   
- Physical plan = optimized seqence of steps(and it will know which node will execute which part of transformations) for nodes in the cluster.   
- Optimizations such as: avoiding multiple passes over the data or pushing down predecates in SQL or chaining multiple predecates or where clauses into one and so on.   
   
### Transformations vs Actions   
   
   
- A transformation descibes how new DFs are obtained (e.g map)   
- Action actually starts executing Spark code (e.g show, count)   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.rv3o8j0t3m.png)   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.mymxbbtheoj.png)   
   
## Joins   
   
Combine data from multiple DataFrames   
   
   
- one(or more) columns from table 1 (left) is compared with one(or more) columns from table 2 (right)   
- if the condition passes, rows are combined   
- non-matching rows are distracted   
   
In Spark, Joins are Wide transformations(read: expensive\!)   
In order to compute a join, Spark scans the entire DFs from the entire clusters and the data is going to be moved around in between nodes, this involves shuffling which is expensive (in terms of performance).