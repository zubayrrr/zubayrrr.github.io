---
created: '2022-04-01T00:00:00.000Z'
desc: ''
id: pgrgb9mbd2wnalfttolc77i
tags:
- tidbits
title: Set a folder to be ignored by Dropbox
updated: 1652815757194
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
## Set to ignore   
   
`attr -s com.dropbox.ignored -V 1 /path/to/dir`   
   
## Set to un-ignore   
   
`attr -r com.dropbox.ignored`