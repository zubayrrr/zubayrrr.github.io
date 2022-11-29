---
created: 20211115150437750
desc: ''
id: q9l2kjgosndymzvlre2b3zs
title: DataFrame
updated: 1653305106664
---
   
Topics::  [apache spark](../topics/apache%20spark.md)   
   
   
---   
   
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