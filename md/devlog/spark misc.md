---
created: 20211118181138000
desc: ''
id: h0jp44pm8khupz9s02ebax4
title: Spark Misc
updated: 1653305106670
---
   
Topics::  [apache spark](../topics/apache%20spark.md)   
   
   
---   
   
`spark.conf.set("spark.sql.legacy.timeParserPolicy","LEGACY")`   
   
Ref:   
   
   
- <[https://youtu.be/sGkkUpdWfLQ>](https://youtu.be/sGkkUpdWfLQ>)   
- <[https://github.com/oliversavio/youtube-vid-code/tree/main/spark-shell>](https://github.com/oliversavio/youtube-vid-code/tree/main/spark-shell>)   
   
`spark-shell --packages com.databricks:spark-xml_2.12:0.12.0`   
   
    scala> import com.databricks.spark.xml._   
   
    scala> val df = spark.read.option("rowTag", "book").xml("books.xml")   
    scala> :paste   
    // Entering paste mode (ctrl-D to finish)   
   
    import org.apache.spark.sql.types._   
    val customSchema = StructType(   
    Array(   
    StructField("title", StringType, nullable=true),   
    StructField("price", DoubleType, nullable=true)   
    )   
    )   
   
    scala> val df = spark.read.option("rowTag","book").schema(customSchema).xml("books.xml")   
   
    scala> df.show   
    scala> df.printSchema