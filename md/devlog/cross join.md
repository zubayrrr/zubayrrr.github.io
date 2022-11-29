---
created: 20211106113626600
desc: ''
id: a72fnt5xrlvy9dg40val25v
title: CROSS JOIN
updated: 1653304922231
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
Cross joins are used to combine every records from the first table with every record in the second table.   
   
    SELECT   
        c.first_name AS customer,   
        p.name AS product   
    FROM customers c   
    CROSS JOIN products p   
    ORDER BY c.first_name   
   
The implicit syntax for CROSS JOIN:   
   
    SELECT   
        c.first_name AS customer,   
        p.name AS product   
    FROM customers c, orders o   
    ORDER BY c.first_name