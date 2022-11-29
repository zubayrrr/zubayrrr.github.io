---
created: 20211105172925504
desc: ''
id: gt8pcjl3aqwp5i47caqt2lq
title: IS NULL
updated: 1653437762206
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
The `IS NULL` operator is used to test for empty values ([NULL](../devlog/null.md) values).   
   
    SELECT *   
    FROM customers   
    WHERE phone IS NULL   
   
using with NOT operator   
   
    SELECT *   
    FROM customers   
    WHERE phone IS NOT NULL