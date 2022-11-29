---
created: 20211107092245284
desc: ''
id: hhtrj9tg5h3mmfjw4cv8w2n
modified: 20211107094521304
title: INSERT INTO
updated: 1653304922126
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
Using `INSERT INTO`   
   
Order of the values should correspond columns in the table   
   
### Insert rows into a table   
   
    INSERT INTO customers   
    VALUES (   
        DEFAULT,   
        "John",   
        "Smith",   
        NULL,   
        DEFAULT,   
        'This house NO.',   
        'This city',   
        'CC',   
        '0'   
    )   
   
    -- the first DEFAULT is for the AUTO_INCREMENT   
    -- CC stands for state code as our table only accepts 2 VARCHAR for state column   
   
To skip the default values and specify columns that you'd like to add, order doesn't matter in this case.   
   
    INSERT INTO customers (   
        first_name,   
        last_name,   
        address,   
        city,   
        country   
    )   
    VALUES (   
        "John",   
        "Smith",   
        'This house NO.',   
        'This city',   
        'CC',   
        '0'   
    )   
   
### Insert multiple rows into a table   
   
    INSERT INTO shippers (name)   
    VALUES   
        ('Shipper1'),   
        ('Shipper2'),   
        ('Shipper3')   
   
### Insert data into multiple tables   
   
    INSERT INTO orders (customer_id, order_date, status)   
    VALUES (   
        1, '2019-01-02', 1   
    )   
    INSERT INTO order_items   
    VALUES   
        (LAST_INSERT_ID(), 1, 1, 2.95),   
        (LAST_INSERT_ID(), 2, 1, 5.5)   
   
`LAST_INSERT_ID()` is a builtin function returns the value of the ID that was last inserted