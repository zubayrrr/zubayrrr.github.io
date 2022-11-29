---
aliases:
- ServiceNow.convert date to ISO ISO8601 format
- Convert Date To ISO ISO8601 Format
category: '2022'
created: 1667343261225
desc: ''
id: 08dde7f1-c211-4dbe-9506-f309a685cf2a
tags:
- tidbits
title: Convert Date To ISO ISO8601 Format
updated: 1667343261225
---
   
Related::  [languages.javascript](../devlog/languages.javascript.md)   
   
   
---   
   
```javascript
var original = '2020-09-18 07:41:40';
var dt = original.split(' ');
var f = dt[0].split('-');
var t = dt[1].split(':');
var event = new Date(f[0], f[1]-1, f[2], t[0], t[1], t[2]);

var isoDate = event.toISOString();
gs.info('iso date:' + isoDate);
```
