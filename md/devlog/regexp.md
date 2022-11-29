---
created: 20211105165305136
desc: ''
id: 8ja424y2w26yowahv1gdr14
title: REGEXP
updated: 1653304922287
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
[MySQL](../devlog/mysql.md) supports another type of pattern matching operation([LIKE](../devlog/like.md)) based on the [regular expression](../devlog/regular%20expression.md)s that is REGEXP operator   
   
   
- It provide a powerful and flexible pattern match that can help us implement power search utilities for our database systems.   
- REGEXP is the operator used when performing regular expression pattern matches. [RLIKE](/not_created.md) is the synonym.   
- It also supports a number of metacharacters which allow more flexibility and control when performing pattern matching.   
- The backslash is used as an escape character. It’s only considered in the pattern match if double backslashes have used.   
- Not case sensitive.   
   
<!-- end list -->   
   
    SELECT *   
    FROM customers   
    WHERE last_name LIKE '%field%'   
   
Instead of using [LIKE](../devlog/like.md)we can use REGEXP such as:   
   
    WHERE last_name REGEXP 'field'   
   
### Patterns   
   
   
- caret(^) matches beginning of the string   
- dollar sign($) matches end of the string   
- p1|p2|p3, pipe matches any of the patterns p1, p2, or p3; Alternation   
- `[]` - Any character listed between the square brackets   
  - `WHERE last_name REGEXP '[gim]e'` searches for last name that ends in `e` but has any of the characters mentioned in the brackets before it.   
  - `'[a-h]e'` will look for all characters from a to h before e