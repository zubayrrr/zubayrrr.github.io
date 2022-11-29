---
created: 20211105151523730
desc: ''
id: lwybnx5oi4zy5x8triu0de4
title: AND OR NOT
updated: 1661077157284
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
   
---   
   
### AND   
   
`WHERE birth_date > '1990-01-01' AND points > 1000` both the conditions have to be true for the [WHERE](../devlog/where.md) clause to return   
   
### OR   
   
`WHERE birth_date > '1990-01-01' OR points > 1000` either of the conditions have to be true for the [WHERE](../devlog/where.md) clause to return   
   
`WHERE birth_date > '1990-01-01' OR points > 1000 AND state = 'VA'`   
   
Order of these operators matter   
   
AND is always evaluated first, OR is evaluated at second priority.   
Use paranthesis to override the precedence   
   
`WHERE birth_date > '1990-01-01' OR (points > 1000 AND state = 'VA')`   
   
### NOT   
   
NOT is used to negate a condition.   
   
`WHERE NOT (birth_date > '1990-01-01' OR points > 1000)` basically inverts the condition that was used. OR becomes AND, `>` becomes `<=`   
   
### Example   
   
    USE store   
   
    SELECT *   
    FROM order_items   
    WHERE order_id = 6 unit_price * quantity > 30