---
created: 20211129220848850
desc: ''
id: lz322a84xc913sor5r5c71u
title: Data Warehouse
updated: 1653318683914
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
   
- A data warehouse is quite literally a large warehouse filled with data.   
- It is not the same as a database.   
- A data warehouse is typically built on some form of database.   
- A database is a platform and the usage of it can be defined as the data warehouse.   
- We don't create the data for the first time in a data warehouse, rather, it is created/brought in by external sources or our operational system send this data to our data warehouse.   
- There is a linear relationship between data sources and data warehouse. The more data sources, the more complex the data warehouse.   
- Data is copied, not moved.(Copies of data is sent into the warehouse)   
   
### It is more than just a storage for data:   
   
   
- A datawarehouse is an integrated environment; data from a number of sources is sent into a data warehouse.   
- Data warehouse should be subject oriented, regardless of how many systems the data is coming from.   
- Time variant   
  - Data warehouse should contain historical data and not just current data.   
- Non volatile   
  - Traditionally, we periodically bring in data into our data warehouse, we do it in batches.   
  - Our data warehouse should remain stable during and between these refreshes and updates.   
   
### Reasons why we build a data warehouse:   
   
   
- Making data-driven decisions   
  - Viewing into the past, present and future; and even the unknwon for Business Intelligence   
- One stop shopping   
  - Integrating data into one place for convenience (that would be lost if we were to constantly work on gathering scattered data)   
   
### Comparing a Data Warehouse to a [Data Lake](/not_created.md)   
   
   
- Traditionally data warehouse are built on top of RDBMS(Microsoft SQL Server, Oracle, DB2)   
- RDBMS are also used in transactional systems and other various settings.   
- Data Warehouse are sometimes also built on top of [MDBMS](../devlog/mdbms.md)(Multi Dimensional Database Management Systems), colloquiolly known as "Cubes" that are special purpose databases   
   
Data Lakes   
   
   
- on the other hand are built on top of some sort of [Big Data](../devlog/big%20data.md) environment rather than a traditional relational data.   
- Some people say that Data Lakes are the next generation of Data Warehouses.   
   
### Comparing Data Warehouse to Data Virtualization   
   
   
- In the days before Data Warehouses, data driven decision making was often done using "Extract Files", which were sort of like mini data warehouses, pulling data from one another but mostly without any data coordination and structure to it's queries. which led to far more time gathering, organizing, reorganizing data than actually analyzing data.   
- Then came on the scene Distributed DBMS (DDBMS) which was kinda like the 1980s attempt at creating [hdfs](../devlog/hdfs.md) of [hadoop](../devlog/hadoop.md) but it was largely a failure due to the lack of technology available at that time.   
- This led to two paths:   
  - Data Warehousing   
  - Data Virtualization   
   
### Data Virtualization   
   
   
- Read-only (vs. read-write) DDBMS   
- In-place data access   
- Unlike a Data Warehouse, we do not duplicate the data, instead we access the data from it's source when we need it.   
- Many names over the years:   
  - Virtual Data Warehousing   
  - Enterprise Information Integration(EII)   
  - Enterprise Data Access (EDA)   
- Data Virtualization use cases   
  - Simple transformations   
  - Smaller number of data sources   
  - Relaxed response time   
   
### ETL   
   
#### Extract(ion)   
   
#### Transform(ing)   
   
#### Load(ing)   
   
It stands between Data Sources -\> Data Warehouses -\> Data Marts   
`where -> represents ETL`   
   
   
---   
   
### Staging Layer   
   
   
- "Landing Zone"   
- "E" within ETL   
- There are 2 variations of Staging Layers   
- Your ETL staging layer objective should be "Focus on E with minimal T"   
- There are two types of staging layers   
- Non-persistent staging layer   
- Persistent staging layer   
   
### User Access Layer   
   
   
- Where users go   
- Data Warehouse is really synonymous with User Access Layer   
- Dimensional data   
- Schemas   
   
See also: [Data Warehouse Architecture](../devlog/data%20warehouse%20architecture.md)