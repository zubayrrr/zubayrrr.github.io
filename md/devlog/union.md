---
created: '2021-11-06T00:00:00.000Z'
desc: ''
id: zlqqdzm6i9fcy8j4ua5u575
title: UNION
updated: 1653304922155
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
   
---   
   
Combine rows from multiple tables/queries   
   
    SELECT   
        order_id,   
        order_date,   
        'Active' AS status   
    FROM orders   
    WHERE order_date >= '2019-01-01'   
   
    UNION   
   
    SELECT   
        order_id,   
        order_date,   
        'Archived' AS status   
    FROM orders   
    WHERE order_date > '2019-01-01'   
   
Another example   
   
    SElECT first_name   
    FROM customers   
    UNION   
    SELECT name   
    FROM shippers   
   
The first query being unionized with the second one should return same amount of columns.   
   
Name of the columns returned will be based on the first query.   
   
Order of the query matters.   
   
### Exercise   
   
    USE sql_store;   
   
    SELECT customer_id, first_name, points, 'Bronze' AS type   
    FROM customers   
    WHERE points < 2000   
   
    UNION   
   
    SELECT customer_id, first_name, points, 'Silver' AS type   
    FROM customers   
    WHERE points BETWEEN 2000 AND 3000   
   
    UNION   
   
    SELECT customer_id, first_name, points, 'Gold' AS type   
    FROM customers   
    WHERE points > 3000   
    ORDER BY first_name