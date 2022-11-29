---
category: '2022'
created: 2022-11-10 14:58:09.297000+00:00
id: 6cdf228f-797f-4c2f-84b6-96c24ffa111b
tags:
- devlog
title: GlideAggregate
updated: 2022-11-10 14:58:09.713000+00:00
---
   
   
- It is an extension of [GlideRecord](../devlog/GlideRecord.md) class.   
- Used when performing aggregate queries (count, min, max, sum, avg)   
	- Reports   
	- Calculations   
- It only works on number fields.   
- It is much easier to use  `addAggregate()`, `getAggregate()` methods that GlideAggregate offers than using GlideRecord mehtods `getRowCount()`