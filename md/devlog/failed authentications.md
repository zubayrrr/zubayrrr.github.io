---
created: '2021-10-22T00:00:00.000Z'
desc: ''
id: 43phw5fod5oq1gnkgfgplsf
tags:
- tidbits
title: Failed Authentications
updated: 1653305638881
---
   
   
- `cat -n /var/log/auth.log | grep -a "authentication failure"`   
- `cat -n /var/log/auth.log | grep -a "authentication failure" | wc -1` using [cat](../devlog/cat.md), [grep](../devlog/grep.md) and [[wc]