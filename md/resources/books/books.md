---
category: '2022'
created: 2022-11-03 13:42:11.265000+00:00
id: ecdba807-23e1-4008-805e-e9526b16e497
tags:
- resources
title: Books
updated: 2022-11-03 13:42:11.681000+00:00
---
   
## Read   
   
```dataview
TABLE Title, By as "Author(s)", Topics FROM #books
WHERE Status="#read"
```
   
   
## Partially Read   
   
```dataview
TABLE Title, By as "Author(s)", Topics FROM #books 
WHERE Status="#partially-read"
```
   
   
## Unread   
   
```dataview
TABLE Title, By as "Author(s)", Topics FROM #books 
WHERE Status="unread"
```
   
   
## Resources   
   
   
- [Books - Commoncog](https://commoncog.com/tag/books/)