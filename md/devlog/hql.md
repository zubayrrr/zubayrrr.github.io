---
created: '2021-11-22T00:00:00.000Z'
desc: ''
id: e92qvq2zwoa9wyn0p0187l3
title: HQL
updated: 1653305310640
---
   
[hive](../devlog/hive.md) Query Language   
   
[hadoop](../devlog/hadoop.md) needs to be running to use hive.   
   
Check if hadoop is running with `jps` or `./start-all.sh` from the `$HADOOP_HOME/sbin` dir.   
   
### Managed vs External table   
   
   
- Managed table is totally managed by Hive.   
  - If you drop a managed table, the data in the able will also be dropped (<span class="underline">deleted</span>), unlike an **external table** where the data <span class="underline">would remain</span>.   
   
### Creating a managed table   
   
    CREATE TABLE table_name(data dataType);   
   
### Creating an external table   
   
    CREATE EXTERNAL TABLE table_name(data dataType);   
   
### Loading data into a table (locally)   
   
    LOAD DATA LOCAL INPATH '/path/to/file.csv' INTO TABLE table_name;   
   
### Partitioning   
   
Dividing the table into some parts based on the values of a particular column like date, course, city or country. The advantage of partitioning is that since the data is stored in slices, the query response time becomes faster.   
   
### Creating partitioned tables   
   
First set these   
   
    set hive.exec.dynamic.partition=True;   
    set hive.exec.dynamic.partition.mode=nonstrict;   
   
Create tables   
   
    create table table_name_partitioned(data dataType)   
    partitioned by (name_of_col string)   
    row format delimited   
    fields terminated by ",";   
   
Loading data into a partitioned table using a csv or other format files or push data   
   
    load data local inpath '/path/to/file.csv' into table_name_partitioned;   
   
Pushing data into a partitioned table   
   
```
insert into table_name_partitioned(name_of_col)
select data from table_name_managed;
```
   
   
This would execute a [mapreduce](../devlog/mapreduce.md) job and when the job ends, it would create folders corresponding to the name of the columns by which the table was partitioned.   
   
### Bucketing   
   
Bucketing in hive is the concept of breaking data down into ranges, which are known as buckets, to give extra structure to the data so it may be used for more efficient queries. The range for a bucket is determined by the hash value of one or more columns in the dataset (or Hive metastore table). These columns are referred to as `bucketing` or `clustered by` columns.   
   
`set.hive.enforce.bucketing=True;`   
   
Creating a bucketed table   
   
    create table table_name_bucketed(data dataType)   
    clustered by (name_of_col string)   
    row format delimited   
    fields terminated by ','   
   
### Partitioning vs. Bucketing   
   
Bucketing is similar to partitioning – in both cases, data is segregated and stored – but there are a few key differences. Partitioning is based on a column that is repeated in the dataset and involves grouping data by a particular value of the partition column. While bucketing organizes data by a range of values, mainly involving primary key or non-repeated values in a dataset.   
   
Partitioning is most effective for low volume data, as it carries the possibility of too many small partition creations and too many directories. And since bucketing results in equal volumes of data in each partition, joins at Map side will be quicker.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.8a2a68hilaj.png)   
   
A table can have both partitions and bucketing info in it; in that case, the files within each partition will have bucketed files in it. For example, if the above example is modified to include partitioning on a column, and that results in 100 partitioned folders, each partition would have the same exact number of bucket files – 20 in this case – resulting in a total of 2,000 files across all partitions.   
   
> via - <[https://www.okera.com/blogs/using-apache-hive-bucketing-with-okera/>](https://www.okera.com/blogs/using-apache-hive-bucketing-with-okera/>)