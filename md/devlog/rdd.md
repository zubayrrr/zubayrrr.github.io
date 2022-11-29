---
created: '2021-11-22T00:00:00.000Z'
desc: ''
id: 2vn2g9mhmi624b83rl5se0k
title: RDD
updated: 1653305226820
---
   
Topics::  [apache spark](../topics/apache%20spark.md)   
   
   
---   
   
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