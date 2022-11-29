---
created: 1661073964559
desc: ''
id: 2fwpqfipn18deinlkqecmii
tags:
- topics
title: Databases
updated: 1661077568926
---
   
Databases are used in applications to persist data.   
   
When your software has the ability to create, update, delete data on your software you need a database for that.   
   
1. Developers need database locally installed for local development.   
2. They can use a database hosted somewhere else remotely.   
   
How does an App talk to a DB ?   
   
   
- In your application code you configure the DB connectivity.   
- Each programming language has a library/module for DB connection.   
- You tell the library, which DB to talk to (**database endpoint**) and how to authenticate with that DB (credentials).   
- It is a best practice to not hardcoded the credentials and database endpoint and instead use environment variables   
- Depending on the environment(Dev, Prod, Test), the environment variables will differ.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661076028/wiki/te1puaei1ejbsjfnrotb.png)   
   
## Database Types   
   
   
- Key Value   
  - [redis](../devlog/Redis.md)   
  - [memcached](/not_created.md)   
  - [kubernetes](/not_created.md)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661076354/wiki/msztvoz3c8zsxaaq1vpr.png)   
   
No joins, very fast, store data in memory (not on harddisk). Limited storage(not fit for primary DBs), they’re usually used as caching DBs on top of a primary DB(long term storage). It can also be used as message queue.   
   
   
- Wide Column   
  - [cassandra](/not_created.md)   
  - [hbase](/not_created.md)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661076486/wiki/arzkkj5evwutmtesicow.png)   
   
Schema-less, any number of column of any data type. Can handle unstructured data with dynamic number of columns per key. Very scalable, easily distribute-able across many servers. No joins. Limited when compared to relational DBs. Query language similar to SQL. Best used for time-series, records from [IoT](../devlog/iot.md) devices, historical data. Best used on top of a primary DB.   
   
   
- Document Database   
  - [mongoDB](../devlog/mongoDB.md)   
  - [DynamoDB](/not_created.md)   
  - [CouchDB](/not_created.md)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661076743/wiki/rj9wa4avj7g1nbmhl0g1.png)   
   
Documents are containers for key-value pairs. Unstructured data, schema-less, documents are grouped in collections and collections can be organized in a relational hierarchy. This mimics a relational DB model but you still get no joins. Slower to update (writes) than relational DB as data is nested within the hierarchy of documents but faster to read. Denormalized. Easy to get started. Best used for: Mobile apps, game apps, CMS. It is much more general purpose. Can be used as primary DB. Shouldn’t be used when data is going to be correlated with one another.   
   
   
- Relational DB   
  - [mysql](../devlog/mysql.md)   
  - [PostgreSQL](../devlog/PostgreSQL.md)   
   
Most widely used and popular. It is a structured DB. It cannot be used for unstructured database as it requires strict schema upfront. You first need to create a schema how the data will look like before you start using it. It uses [languages.sql](../devlog/languages.sql.md).   
   
In relational databases, data is organized in tables which has rows and columns.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661077594/wiki/okwhx744kmoydvefplsy.png)   
   
Normalized to avoid duplicate data. They’re ACID compliant.   
   
ACID = Atomicity, Consistency, Isolation, Durability. (data consistency  and validacy is guaranteed).   
   
No half changes are updated in the DB. When there is a disruption during an update the changes are rolled back.   
   
Either all changes are applied or none. Important for banking and other financial services.    
   
Difficult to scale.  Running them on a distributed and containerized environments can be challenging.   
   
Theres [cockroachDB](/not_created.md) to solve scalability problem.   
   
Because of it’s popularity relational DBs vs NON-relational DB are referred to as **SQL VS NOSQL**.   
   
   
- Graph DB   
	- [Neo4j](/not_created.md)   
	- [Dgraph](/not_created.md)   
   
Directly connect entities, edges are the relationships. Easier to query related data as compared with relational DB. Nodes and Edges are used.   
   
Best used for detecting  patterns in the application data and detecting relations between records. Things like recommendation engines.   
   
   
- Search DB   
	- [Elasticsearch](../devlog/Elasticsearch.md)   
	- [solr](/not_created.md)   
Search database through massive data entries(think search engines). Full text search in efficient and fast way. They work similar to document oriented database, the difference is that the search DB in the BG analyses data and creates index of all individual words.   
   
When user searched it only searches in the index it developed.