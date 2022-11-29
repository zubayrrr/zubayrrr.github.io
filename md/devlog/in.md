---
created: 20211105153933804
desc: ''
id: c3nbgvzl9k9ewr8g3338eud
title: IN
updated: 1653304922324
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
The IN command allows you to specify multiple values in a WHERE clause.   
The IN operator is a shorthand for multiple OR conditions.   
   
Compare an attribute with a list of values   
   
    SELECT *   
    FROM customers   
    WHERE state = 'VA' OR state = 'GA' OR state = 'FL'   
   
Can be written instead as   
   
    SELECT *   
    FROM customers   
    WHERE state IN ('VA', 'FL', 'GA')2   
   
   
    -- the order doesn't matter   
    -- NOT can also be used  such as   
   
    WHERE state NOT IN ('VA', 'FL', 'GA')   
   
### Example   
   
    SELECT *   
    FROM products   
    WHERE quantity_in_stock IN (49, 38, 72)