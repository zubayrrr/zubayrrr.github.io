---
created: 20211105173719776
desc: ''
id: ebdna3cjeqhx91iheag3edr
title: ORDER BY
updated: 1661077144687
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
The `ORDER BY` keyword is used to sort the result-set in ascending or descending order.   
   
The `ORDER BY` keyword sorts the records in ascending order by default. To sort the records in descending order, use the `DESC` keyword.   
   
Sort by colum other than default sort column with `ORDER BY`; in relational databases every table has a primary key column and it uses that for default sort. The values should uniquely identify the other records in the table.   
   
    SELECT *   
    FROM customers   
    ORDER BY first_name   
   
   
    --or use DESC to sort it in descending order   
    ORDER BY first_name DESC   
   
   
    --or   
    ORDER BY state, first_name   
   
   
    --or   
   
    ORDER BY state DESC, first_name   
   
In [MySQL](../devlog/mysql.md) we can sort data by any columns wether or not it was [select](../devlog/select.md)ed in the SELECT clause.   
   
    SELECT first_name, last_name   
    FROM customers   
    ORDER BY birth_date   
   
Data can also be sorted by an alias   
   
    SELECT first_name, last_name, 10 AS points   
    FROM customers   
    ORDER BY points, first_name   
   
Sort by columns as [select](../devlog/select.md)ed   
   
    SELECT first_name, last_name   
   
    --where first_name is 1 and last_name 2   
    ORDER BY 1, 2   
   
    --sorting like this is discouraged