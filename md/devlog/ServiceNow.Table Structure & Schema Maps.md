---
created: 1663392745567
desc: ''
id: 4g0wdr6xctijepom89y1sf1
title: Table Structure & Schema Maps
updated: 1663392757262
---
   
## Table Relationships   
   
Example:   
   
- Person table has _first name_ and _last name_ fields.   
- Student and Faculty tables extend Person table, thus Student and Faculty tables inherit _first name_ and _last name_ fields.   
   
We have the Person table to avoid redundancies and add extensibility.   
Table relationships are very common and important in CMDB.   
   
A CMDB has hundreds of tables that are related to one another which allows ServiceNow to create “Business Service Maps”.   
   
Relationships can be one-to-many or many-to-many.   
   
Example for one-to-many:   
   
Every table one or more fields, every field belongs to only one table.   
   
Example for many-to-many:   
   
Each User can have many Groups, each Group may have many Users.   
   
## CMDB Tree Structure   
   
   
- Majority of tables extend `cmdb_ci` table such as `cmdb_ci_server` and `cmdb_ci_appl`.   
- New CI classes extend `cmdb_ci` table.   
   
## Tables & Columns Module   
   
   
- Great for exploring tables and fields   
- List field attributes   
- Link to schema map   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663393357/wiki/tuceeecrxlu3fumjnowx.png)   
   
## Schema Map   
   
   
- It is a diagram that visualizes table relationships   
- We can _focus_ on a table and the schema map will show all tables that extend or are _extended_   by the focused table as well as referenced table.   
- It can be helpful to conceptualize the relationship between multiple tables.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663394259/wiki/ci81px0a8p9daczlogln.png)   
   
Schema Map is currently throwing an error on San Diego…possibly a bug…might be fixed later.    
   
## Business Service   
   
Dependency Maps   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663394543/wiki/a2ngwwaff7jiavv1ovfk.png)