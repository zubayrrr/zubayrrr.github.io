---
created: 20211105135219492
desc: ''
id: s7192pva5ewna1wqsaglkqn
title: SELECT
updated: 1661077184289
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
   
---   
   
To retrieve data from a single table:   
   
   
- select the database to retrieve data from(in other words, to run a query against) by using the [USE](/not_created.md) keyword, once selected, the database selected will be displayed in **bold** on workbench navigator panel.   
- `USE database;`   
- `SELECT column_1, column_2`   
- `SELECT *` to select all columns   
- `FROM table_name` using the [FROM](/not_created.md) clause   
   
Example:   
   
    USE store;   
    SELECT * FROM customers   
   
Using other (optional) clauses such as [WHERE](../devlog/where.md) and [[ORDER BY](/not_created.md)   
   
To only return customer with id = `1` and sort by first name, `--` double hyphen to comment something out   
   
    USE store;   
    SELECT *   
    FROM customers   
    WHERE customer_id = 1   
   
    -- WHERE customer_id = 1   
    ORDER BY first_name   
   
   
- Use `SELECT *` to get all columns   
- You can specify colums by:   
  - `SELECT column_1, column_2` you can also put different columns on different lines   
    - The order of the columns specified matters   
- You can do arithemtic operations on a column   
  - `SELECT numbers + 10`   
  - `SELECT (numbers + 100) * 10` the order of operators matter, use paranthesis to change the order of operations and to also add readability.   
  - `SELECT numbers + 10 AS new_numbers` to add an alias   
- To remove duplicates use:   
  - `SELECT DISTINCT column_name`   
   
See also: [WHERE](../devlog/where.md)