---
created: 20211022180919380
desc: ''
id: en7wdmf7rc8a7l3s8940klv
tags:
- tidbits
title: Get MAC Address from ifconfig
updated: 1652818339102
---
   
Topics::  [networking](../topics/networking.md)   
   
   
---   
   
`ifconfig | grep ether | cut -d" " -f10`     
using [cut](../devlog/cut.md), [ifconfig](../devlog/ifconfig.md), [grep](../devlog/grep.md)