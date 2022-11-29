---
created: 20211105145341976
desc: ''
id: 9yss2lq8hxniiu82ai30yvl
title: WHERE
updated: 1653304922306
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
WHERE returns only true conditions, it is used to filter data, query execution engine iterates and checks(evaluates) the condition and returns if true.   
   
```sql
SELECT *
    FROM customers
    WHERE points > 3000`
```
   
   
We can use [Relational operators](../devlog/relational%20operators.md) for comparison   
   
`<>` is also a "not equals to" operator   
   
Enclose your string values inside single or double quotes:   
   
`WHERE state = 'VA'` - it is not case sensitive   
   
`WHERE birth_date > '1990-01-01' that is YYYY-MM-DD, dates are treated as strings in [[sql]]`