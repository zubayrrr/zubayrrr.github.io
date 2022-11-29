---
created: 20211110193258068
desc: ''
id: 30isnfzmqrvmmiii03d0chj
title: Hive
updated: 1653318643715
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
   
- Hive: It is a platform used to develop [languages.sql](../devlog/languages.sql.md) type scripts to do MapReduce operations.   
- Hive is a data warehouse infrastructure tool to process <span class="underline">structured data</span>(data stored in rows and columns) in Hadoop. It resides on top of Hadoop to summarize Big Data, and makes querying and analyzing easy.   
  - Initially Hive was developed by Facebook, later the Apache Software Foundation took it up and developed it further as an open source under the name Apache Hive. It is used by different companies. For example, Amazon uses it in Amazon Elastic MapReduce.   
- It stores schema in a database and processed data into HDFS.   
- It is designed for OLAP.   
- Good for batch processing.   
- It provides SQL type language for querying called HiveQL or [HQL](../devlog/hql.md).   
- It is familiar, fast, scalable, and extensible.   
- Parallel computing(since it uses HDFS).   
- Supports partitions.   
- Supports bucketing.   
   
[hadoop](../devlog/hadoop.md) = [hdfs](../devlog/hdfs.md) + [mapreduce](../devlog/mapreduce.md)   
   
[hdfs](../devlog/hdfs.md) - where your data gets distributed and [mapreduce](../devlog/mapreduce.md) is where you write transformation jobs using java and MR will do distributed processing by reading the data from HDFS.   
   
In MR you cannot write any SQL, you'll have to use Java for queries   
   
A SQL layer was introduced to communicate with MR   
   
Hive is a query engine, it is not a DB. It doesn't have it's own storage to store data, Hive uses HDFS to store data.   
   
It runs on Engine MR, often called as an Abstraction of MR.   
Internally it uses MR engine to process queries.   
   
Hive replaces the Java part that was required to write SQL in MR.   
   
Hive can also run on Spark Engine not just MapReduce(MR)   
   
   
---   
   
Send a request to Hive Server, create table test. hive stores metadata; all the table information. This metadata is different from what is stored on Master node.   
   
Hive metadata is stored in an RDBMS(Oracle, MySQL etc) known as Remote meta store , the data is stored in HDFS.   
   
When you request hive to load or insert data, it'll get the metadata info about the table and based on that schema it'll store data on HDFS.   
   
When you request hive to select, hive will first query the metadata info and then get the data from HDFS and display's data in tables.   
   
They decoupled the metadata from hive and use RDBMS for it.   
   
When there is no RDBMS provided for Hive, it in that case the metadata will be stored on an embedded RDBMS known as `Derby`, it comes along with Hive, doesn't have to be installed separately. Derby cannot be replaced. Embedded meta store, remote meta store.   
   
Remote meta store uses separate instance of RDBMS to store data, it is the most common in the real world. The embedded meta store will create problem when you have multiple machines(a cluster) running instances of Hive, multiple embedded meta store on nodes will create synchronization problems. You cannot make a distributed request. Hence a remote meta store is used.   
   
All the nodes(that are running Hive) will refer to a node that is running an RDBMS. The configuration file(s, on each Hive node), derby will be removed automatically once you select RDBMS on the config file.   
   
Embedded meta store is good for practicing on a single node,   
   
a [JDBC](/not_created.md) connection can also be made.   
   
Hive can also be used with S3.   
   
### Limitations   
   
   
- It is not an OLTP system.   
- Not for real-time processing   
- Doesn't support full fledged [languages.sql](../devlog/languages.sql.md) queries (such as some joins, triggers)