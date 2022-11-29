---
created: 20211107114041660
desc: ''
id: p5jw4wchevr9jx8inug22qo
title: DELETE FROM
updated: 1653304922284
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
We use `DELETE FROM` statement to delete records from a table   
   
    DELETE FROM invoices   
   
    -- WHERE can be optionally used to search and filter out results to delete   
    WHERE client_id =   
   
    -- using subquery   
    (SELECT *   
    FROM clients   
    WHERE name = 'Myworks')