---
created: '2021-11-30T00:00:00.000Z'
desc: ''
id: ffhm4kotv5wbd139ml9ch44
title: ETL
updated: 1653318670590
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
ETL stands for **E**xtract(ion) | **T**ransform(ing) | **L**oad(ing)   
   
This process stands between Data sources and [data warehouse](../devlog/data%20warehouse.md)   
   
It is a data flow technique   
   
### Extract   
   
   
- Quickly pull data from various source applications.   
- Traditionally done in "batches" (every hour, day, week, mins or other intervals).   
- ETL is known as batch oriented data flow process.   
- When data is first brought in, it is in raw form(at); errors and all.   
- Land in data warehouse staging layer.   
   
### Transform   
   
   
- "Apples to apples"   
- Prepare for uniform data in user access layer   
- It can be very complex   
   
### Load   
   
   
- Final stop along the data pathway   
- Store uniform data in user access layer   
   
### Challenges with traditional ETL   
   
   
- Significant business analysis before storing data   
- Significant data modeling before storing data   
   
### ELT   
   
   
- "Blast" data into [Big Data](../devlog/big%20data.md) environment.   
- Bring in data in raw form in [hadoop](../devlog/hadoop.md), [hdfs](../devlog/hdfs.md), AWS S3, etc.   
- Use big data environment computing power to transform when needed.   
- "Schema on read" (ETL) vs "Schema on write" (ELT)   
- Mostly used when creating a [Data Lake](/not_created.md) or hybrid data lakes.   
   
   
---   
   
There are two types of ETL: _Initial_ Incremental   
   
### Initial ETL   
   
   
- Normally one time only   
- Right before the data warehouse goes live   
- All relevant data necessary for BI and analytics   
- Redo if data warehouse "blows up"   
   
### Incremental ETL   
   
   
- Incrementally "refreshes" the data warehouse   
- New data: employees, customers, products ...   
- Modified data: employee promotions, product price, change..   
- Special handling for deleted data: customer drops from a subscription plan...(not actually deleting)   
- Four major incremental ETL patterns   
  - Append   
  - In-place update (going into existing rows of data and updating them)   
  - Complete replacement   
  - Rolling append(maintaing a certain duration of history and wiping old data)   
- Most Incremental ETL done today is comprised only of:   
  - Append   
  - In-place update   
   
### Common transformation models   
   
   
- Data value unification   
- Data type and size unification   
- De-duplication   
- Dropping Columns(vertical slicing)   
- Value-based row filter(horizontal slicing)   
- Correcting known errors