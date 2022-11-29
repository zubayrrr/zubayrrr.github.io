---
created: '2021-11-07T00:00:00.000Z'
desc: ''
id: fwqpd8xjwd2enq3xbu37dmp
title: UPDATE
updated: 1661077197824
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
   
---   
   
### Updating a single row   
   
Using `UPDATE` and [SET](/not_created.md) clause   
   
    UPDATE invoices   
    SET payment_total = 10, payment_date = "2019-03-01"   
    WHERE invoice_id = 1   
   
Restore values   
   
    UPDATE invoices   
    SET payment_total = DEFAULT, payment_date = NULL   
    WHERE invoice_id = 1   
   
Modifying existing row   
   
    UPDATE invoices   
    SET   
        payment_total = invoice_total * 0.5,   
        payment_date = due_date   
    WHERE invoice_id = 1   
   
### Updating multiple rows   
   
[MySQL](../devlog/mysql.md) workbench by default works in safe-mode and doesn't allow updating of multiple rows, remove this setting from   
`Workbench Preferences > SQL Editor > uncheck Safe Updates` and restart client.   
   
    UPDATE invoices   
    SET   
        payment_total = invoice_total * 0.5,   
        payment_date = due_date   
    WHERE client_id = 3   
   
    -- WHERE client_id IN (3, 4)   
    -- To update all records in the table, remove the WHERE clause   
   
### Exercise   
   
    USE sql_store;   
   
    UPDATE customers   
    SET points = points + 50   
    WHERE birth_date < "1990-01-01"   
   
### Using Subqueries in updates   
   
Using Subquery to use client's name for fetching their ID   
   
    UPDATE invoices   
    SET   
        payment_total = invoice_total * 0.5,   
        payment_date = due_date   
    WHERE client_id =   
                (SELECT client_id   
                FROM clients   
                WHERE name = 'Myworks')   
   
When a subqery returns multiple records, we cannot use `=` in the WHERE clause, replace it with an [IN](../devlog/in.md) operator instead   
   
    UPDATE invoices   
    SET   
        payment_total = invoice_total * 0.5,   
        payment_date = due_date   
    WHERE client_id IN   
                (SELECT client_id   
                FROM clients   
                WHERE state IN ('CA', 'NY'))   
   
### Exercise   
   
    USE sql_store;   
   
    UPDATE orders   
    SET   
        comment = "Gold Customer"   
    WHERE customer_id IN   
        (SELECT customer_id   
        FROM customers   
        WHERE points > 3000)