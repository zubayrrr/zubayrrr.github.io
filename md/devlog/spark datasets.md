---
created: 20211118200059780
desc: ''
id: mtez5e789o0yozjrbt75wua
title: Spark Datasets
updated: 1653305106650
---
   
Topics::  [apache spark](../topics/apache%20spark.md)   
   
   
---   
   
DataFrame – It works only on structured and semi-structured data. It organizes the data in the named column. ... DataSet – It also efficiently processes structured and unstructured data. It represents data in the form of JVM objects of row or a collection of row object.   
   
> via — <[https://data-flair.training/blogs/apache-spark-rdd-vs-dataframe-vs-dataset>](https://data-flair.training/blogs/apache-spark-rdd-vs-dataframe-vs-dataset>)   
   
They're distributed collections of JVM objects instead of distributed collections of untyped rows, they're essentially <span class="underline">typed dataframes</span>.   
   
They're most useful when: \* We want to maintain type information/type safety \* We want to maintain clean and concise code (especially in production) \* Very effective when we want our filters/transformations are hard to express in DF or SQL.   
   
A more powerful version of Dataframes because we also have types.   
   
Avoid when:   
   
   
- Performance is critical: Spark can't optimize transformation   
  - All those transformations or filters are actually plain Scala objects, that will be evaluated at run-time, after Spark has the chance to plan for the operations in advance, Spark would have to evaluate all filters/transformations on row by row basis(which is slow).