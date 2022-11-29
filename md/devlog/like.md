---
created: 20211105155748908
desc: ''
id: d7h99jjn2d17ybx1f4pj57c
title: LIKE
updated: 1661077210819
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
   
---   
   
The LIKE command is used in a [WHERE](../devlog/where.md) clause to search for a specified pattern in a column.   
   
You can use two wildcards with LIKE:   
   
   
- `%` - Represents zero, one, or multiple characters   
- `_` - Represents a single character (MS Access uses a question mark (?) instead)   
   
Retrive rows that match a specific string pattern.   
   
`WHERE last_name LIKE 'b%'` will return all customers whose last name starts with `b`; doesn't matter if it's an uppercase or a lowercase. `%` can be at the beginning or at the end or like `%b%`   
   
`_` matches a single character, `_y` would check for something thats exactly 2 characters long, the first character is irrelevant but the second character should be `y`   
   
`_____y` to search for something that is six characters long and ends in y   
   
LIKE is older, [REGEXP](../devlog/regexp.md) is newer.   
   
### Examples   
   
    SELECT *   
    FROM customers   
    WHERE address LIKE '%trail%' OR   
                address LIKE '%avenue%'   
   
    SELECT *   
    FROM customers   
    WHERE phone LIKE '%9'   
   
    -- these can also be combined with NOT operator   
   
    WHERE phone NOT LIKE '%9'