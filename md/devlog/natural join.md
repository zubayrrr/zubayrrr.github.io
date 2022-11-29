---
created: 20211106113055600
desc: ''
id: 1io9ap5pqqnrhlpl7o31giw
modified: 20211106113237244
title: NATURAL JOIN
updated: 1653304922221
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
We don't need to explicity define what column names to compare, the engine will look at the tables and join them based on the common columns   
   
    SELECT   
            o.order_id,   
            c.first_name   
    FROM orders o   
    NATURAL JOIN customers c