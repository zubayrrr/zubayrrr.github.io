---
created: 20211105194350020
desc: ''
id: 5eirdrb3hei9f1u2tiqphf4
title: JOIN
updated: 1661077246409
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
### INNER JOIN   
   
   
- `INNER` can be optionally prepended to [JOIN](../devlog/join.md) as there are INNER and OUTER joins in SQL, whenever you type `JOIN` you're using an INNER JOIN by default.   
- joining `orders` table with `customers` table   
   
<!-- end list -->   
   
    SELECT *   
    FROM orders   
    JOIN customers   
   
To line up one table with the other the [ON](/not_created.md) keyword is used so that the records from one table matches with the other, `ON` is followed by a condition on **how** to join the tables   
   
    SELECT *   
    FROM orders   
   
    --columns from orders table are displayed first since it is declared first   
    JOIN customers ON orders.customer_id = customers.customer_id   
   
To display `customer_id` column, the column has to be selected from either the `orders` table or the `customers` table   
   
    SELECT order_id, orders.customer_id, first_name, last_name   
    FROM orders   
    JOIN customers   
            ON orders.customer_id = customers.customer_id   
   
To avoid repetition and make code simpler(more readability), abbreviate table names   
   
    SELECT order_id, o.customer_id, first_name, last_name   
    FROM orders o   
    JOIN customers c   
            ON o.customer_id = c.customer_id   
   
### Example   
   
    SELECT order_id, p.product_id, quantity, o.unit_price   
    FROM order_items o   
    JOIN products p   
            ON o.product_id = p.product_id   
   
   
---   
   
### Joining Across Databases   
   
Your query will be different depending on the current database.   
   
    USE inventory;   
   
    SELECT *   
    FROM store.order_items oi   
    JOIN products p   
            ON oi.product_id = p.product_id   
   
### Self Joins   
   
Join a table with itself   
   
    USE sql_hr;   
   
    SELECT   
            e.employee_id,   
            e.first_name,   
            m.first_name AS manager   
    FROM employees e   
    JOIN employees m   
            ON e.reports_to = m.employee_id   
   
### Joining Multiple Tables   
   
    USE sql_invoicing;   
   
    SELECT   
            p.date,   
            p.invoice_id,   
            p.amount,   
            c.name,   
            pm.name   
    FROM payments p   
    JOIN clients cs   
            ON p.client_id = c.client_id   
    JOIN payment_methods pm   
            ON p.payment_method = pm.payment_method_id   
   
### Compound JOIN conditions   
   
When you have a table with composite primary key, you can join those tables with other tables such as:   
   
    SELECT *   
    FROM order_items oi   
    JOIN order_item_notes oin   
            ON oi.order_id = oin.order_id   
            AND oi.product_id = oin.product_id   
   
### Implicit JOIN syntax   
   
    SELECT *   
    FROM orders o   
    JOIN customers c   
            ON o.customer_id = c.customer_id   
   
The above query can be instead written as:   
   
    SELECT *   
    FROM orders o, customers c   
    WHERE o.customer_id = c.customer_id   
   
Using implicit JOIN syntax is discourged to avoid a "[CROSS JOIN](../devlog/cross%20join.md)", for example, if you removed the [WHERE](../devlog/where.md) clause from the above query, it would match every record on the `orders` table with every record on `customers` table.   
   
   
---   
   
### OUTER JOIN   
   
    SELECT   
            c.customer_id,   
            c.first_name,   
            o.order_id   
    FROM customers c   
    JOIN orders o   
            ON c.customer_id = o.customer_id   
   
    --the above condition will only return customers that have orders placed, for customers that don't have an order id nothing will be returned   
    ORDER BY c.customer_id   
   
There are two types of OUTER JOINs in [MySQL](../devlog/mysql.md)   
   
   
- LEFT JOIN   
- RIGHT JOIN   
   
When you use `LEFT JOIN` all the records from the left table(on the FROM clause) are returned whether the `ON` condition is true or not and this is vice versa for `RIGHT JOIN`   
   
The `OUTER` keyword is optional as long as you're specifying `RIGHT` or `LEFT`   
   
    SELECT   
            c.customer_id,   
            c.first_name,   
            o.order_id   
    FROM customers c   
    LEFT JOIN orders o   
            ON c.customer_id = o.customer_id   
    ORDER BY c.customer_id   
   
### OUTER JOIN between multiple tables   
   
    SELECT   
            c.customer_id,   
            c.first_name,   
            o.order_id,   
            sh.name AS shipper   
    FROM customers c   
    LEFT JOIN orders o   
            ON c.customer_id = o.customer_id   
    LEFT JOIN shippers sh   
            ON o.shipper_id = sh.shipper_id   
    ORDER BY c.customer_id   
   
### Exercise   
   
    SELECT   
        o.order_date,   
        o.order_id,   
        c.first_name,   
        sh.name AS shipper,   
        os.name AS status   
    FROM orders o   
    JOIN customers c   
            ON o.customer_id = c.customer_id   
   
    --using INNER JOIN as the condition is true   
    LEFT JOIN order_statuses os   
            ON o.status = os.order_status_id   
    LEFT JOIN shippers sh   
            ON o.shipper_id = sh.shipper_id   
   
### Self OUTER JOIN   
   
    USE sql_hr;   
   
    SELECT   
            e.employee_id,   
            e.first_name,   
            m.first_name AS manager   
    FROM employees e   
    LEFT JOIN employees m   
            ON e.reports_to = m.employee_id