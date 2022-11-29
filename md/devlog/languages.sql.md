---
created: 20211105134756444
desc: ''
id: 93cp838qc8pnou1we4cbdjb
title: SQL
updated: 1661077304952
---
   
Topics::  [Databases](../topics/Databases.md), [computer science](../topics/computer%20science.md)   
   
   
---   
   
### SQL stands for Structured Query Language, MySQL is a relational database, every(column, row) is related to each other.   
   
SQL is not case sensitive but as an industry standard practice, use uppercase for SQL keywords and lowercase for all the other things when writing queries.   
   
Order of the clauses matter   
   
1.  [select](../devlog/select.md)   
2.  [FROM](/not_created.md)   
3.  [WHERE](../devlog/where.md)   
4.  [ORDER BY](../devlog/order%20by.md)   
   
Line breaks, whitespaces, tabs are ignored when executing SQL code, each clause are written on a new line for better readability.   
   
   
- Composite primary key contains more than one column   
   
## Getting started   
   
To get started, install:   
   
   
- `sudo apt-get install mysql-server mysql-client libmysqlclient-dev`   
- Also install [Mysql Workbench](https://www.mysql.com/products/workbench/)   
- See [Access denied for user 'root'@'localhost'](/not_created.md)   
   
## Retrieving Data From a Single Table   
   
   
- [select](../devlog/select.md) clause   
   
### Combine multiple multiple search conditions when filtering data   
   
   
- The AND, OR and NOT operators   
- [IN](../devlog/in.md) operator   
- [BETWEEN](../devlog/between.md) operator   
- [LIKE](../devlog/like.md)command   
- [REGEXP](../devlog/regexp.md) command   
- [NULL](../devlog/null.md) value   
- [ORDER BY](../devlog/order%20by.md) clause   
- [LIMIT](../devlog/limit.md) clause   
   
   
---   
   
## Retrieving Data From Multiple Tables   
   
   
- [JOIN](../devlog/join.md) operator   
- [USING](../devlog/using.md) clause   
- [NATURAL JOIN](../devlog/natural%20join.md) - not recommend, can produce unexpected results   
- [CROSS JOIN](../devlog/cross%20join.md)   
- [UNION](../devlog/union.md) - combine rows from multiple tables and queries   
   
   
---   
   
## Inserting, Updating, and Deleting Data   
   
### Column attributes   
   
   
- Column name   
- Datatype:   
  - `INT` (whole numbers, no decimals)   
  - `VARCHAR` (variable-characters used for strings, textual values, max length can be assigned inside paranthesis)   
  - `DATE`   
  - `CHAR` (unlike VARCHAR, max length assigned to CHAR is not variable and will be assigned indefinitely no matter the input size of the string)   
- Primary Key   
- [NOT NULL](../devlog/not%20null.md)   
- `AUTO_INCREMENT` (often used with primary key columns, mysql or other engines will auto assign a value)   
- Default values/Expression (can be specified in this column)   
   
## Inserting   
   
   
- [INSERT INTO](../devlog/insert%20into.md)   
   
## Creating   
   
   
- [[CREATE TABLE]   
   
The SELECT clause on the above query is known as a `Subquery`, another example of Subquery:   
   
   
    -- right click on orders_archived table and truncate to delete all records   
    INSERT INTO orders_archived   
    SELECT *   
    FROM orders   
    WHERE order_date < '2019-01-01'   
   
## Updating   
   
   
- [UPDATE](../devlog/update.md)   
   
## Deleting Rows   
   
   
- [DELETE FROM](../devlog/delete%20from.md)   
   
   
---   
   
## Summarizing Data   
   
   
- [Aggregate Functions](../devlog/aggregate%20functions.md)   
- [GROUP BY](../devlog/group%20by.md) clause   
- [HAVING](../devlog/having.md) clause   
- [ROLLUP](../devlog/rollup.md) operator