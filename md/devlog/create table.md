---
created: 20211107101528184
desc: ''
id: pnf9swwp18sfso3vhamq4zo
title: CREATE TABLE
updated: 1653304922117
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
   
---   
   
### Copying data from one table to another   
   
A new table will be created with the exact same values as the `orders` table but the `orders_archived` table will not have the same attributes, the primary key will not be assigned, AUTO_INCREMENT will also be not assigned, if you want to explicitly insert a record into that table, supply a value for `order_id` as its no longer marked for auto completion.   
   
    CREATE TABLE orders_archived AS   
    SELECT * FROM orders   
   
### Exercise   
   
    USE sql_invoicing;   
   
    CREATE TABLE invoices_archived AS   
    SELECT   
        i.invoice_id,   
        i.number,   
        c.name AS client,   
        i.invoice_total,   
        i.payment_total,   
        i.payment_date,   
        i.invoice_date,   
        i.due_date   
   
    -- c.client_id,   
    -- i.client_id,   
    FROM invoices i   
    JOIN clients c   
        USING (client_id)   
   
    -- ON c.client_id = i.client_id   
    WHERE i.payment_total > 0.00   
   
    -- WHERE payment_date IS NOT NULL