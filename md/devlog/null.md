---
created: '2021-11-05T00:00:00.000Z'
desc: ''
id: q93upvd18jszt7x1jl8odp8
title: 'NULL'
updated: 1653304922120
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
A field with a NULL value is a field with no value.   
   
If a field in a table is optional, it is possible to insert a new record or update a record without adding a value to this field. Then, the field will be saved with a NULL value.   
   
Note: A NULL value is different from a zero value or a field that contains spaces. A field with a NULL value is one that has been left blank during record creation\!   
   
It is not possible to test for NULL values with comparison operators, such as =, \<, or \<\>.   
   
We will have to use the [IS NULL](../devlog/is%20null.md) and [IS](/not_created.md) [NOT NULL](../devlog/not%20null.md) operators instead.