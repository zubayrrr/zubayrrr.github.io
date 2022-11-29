---
created: 20211105182541188
desc: ''
id: mb3bmqmvdne6cjgw6k2nvbg
title: LIMIT
updated: 1652622343017
---
   
   
- The LIMIT clause is used to set an upper limit on the number of [tuple](/not_created.md)s or results returned by SQL.   
- It is important to note that this clause is not supported by all SQL versions.   
- The LIMIT clause can also be specified using the SQL 2008 [OFFSET](/not_created.md)/[FETCH](/not_created.md), [FIRST](/not_created.md) clauses.   
- The limit/offset expressions must be a non-negative integer.   
   
  SELECT \*   
  FROM customers   
  LIMIT 3   
   
  --will output only first 3 customers(rows?)   
   
  LIMIT 300   
   
  --if there are 300 customers in the table that will be returned, otherwise only the existing columns will be returned   
   
To use offset (in case of building pagination etc)   
   
    SELECT *   
    FROM customers   
    LIMIT 6, 3   
   
    --will output columns after 6 rows and then return 3 columns   
   
### Example   
   
    SELECT *   
    FROM customers   
    ORDER BY points DESC   
    LIMIT 3   
   
The order of clauses written matters.