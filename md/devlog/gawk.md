---
created: 20211123201345476
desc: ''
id: 8emr5u1zw5qr2hntodgzonr
title: gawk
updated: 1652947230093
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`gawk` or `awk` is a very powerful text processing tool.   
   
### Example   
   
gawk can parse the results of the "uptime" command (uptime provides length of time a Linux server has been running and some other system load data).   
   
Getting the eigth field from the [stdout](../devlog/stdout.md) of [uptime](/not_created.md)   
   
`uptime|sed 's/min,\ //' |sed 's/,//g'|awk '{print $8}'`