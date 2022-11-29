---
created: 20211105154723420
desc: ''
id: 59unjworqzssqywyrxvn2mk
title: BETWEEN
updated: 1653304922321
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
   
---   
   
The BETWEEN command is used to select values within a given range. The values can be numbers, text, or dates.   
   
The BETWEEN command is inclusive: begin and end values are included.   
   
    SELECT *   
    FROM customers   
    WHERE points >= 1000 AND points <= 3000   
   
Can instead be written as   
   
    SELECT *   
    FROM customers   
    WHERE points BETWEEN 1000 AND 3000   
   
### Example   
   
    SELECT *   
    FROM customers   
    WHERE birth_date BETWEEN '1990-01-01' AND '2000-01-01'