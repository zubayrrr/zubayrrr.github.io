---
created: '2021-11-06T00:00:00.000Z'
desc: ''
id: xwraugdlo1ydb128xtit8gy
title: USING
updated: 1661077223589
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
As our queries get more complex, [JOIN](../devlog/join.md) statements can get in the way of readability, to avoid this, we can use `USING`   
   
If the <span class="underline">column name is exactly the same</span> on the `JOIN` (`ON`) statement across two tables, they can be replaced with `USING` such as   
   
    SELECT   
        o.order_id,   
        c.first_name,   
        sh.name AS shipper   
    FROM orders o   
    JOIN customers c   
   
    --ON o.customer_id = c.customer_id can be replaced with   
            USING (customer_id)   
    LEFT JOIN shippers sh   
            USING (shipper_id)   
   
For joining tables with composite primary key and with multiple columns to be compared such as:   
   
```
SELECT *
FROM order_items oi
JOIN order_item_notes oin
        ON oi.order_id = oin.order_id AND
             oi.product_iid = oin.product_id
```
   
   
Can be simplified using `USING`   
   
    SELECT *   
    FROM order_items oi   
    JOIN order_item_notes oin   
            USING (order_id, product_id)   
   
### Exercise   
   
    USE sql_invoicing;   
   
    SELECT   
            p.date,   
            c.name AS client,   
            p.amount,   
            pm.name AS payment_method   
    FROM payments p   
    JOIN clients c   
            USING (client_id)   
    JOIN payment_methods pm   
            ON p.payment_method = pm.payment_method_id