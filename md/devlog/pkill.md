---
created: 20211028140114464
desc: ''
id: ungvanr0fogsuwsbfof5c4x
title: pkill
updated: 1653305490654
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`pkill` is used to send [signal](../devlog/signal.md) to the [process](../devlog/process.md)es of a running program based on given criteria. The processes can be specified by their full or partial names(unlike [killall](../devlog/killall.md)), a user running the process, or other attributes.   
   
`pkill` is basically a wrapper around the [pgrep](../devlog/pgrep.md) program that only prints a list of matching processes.   
   
### Example   
   
   
- `pkill processName` or `pkill partialProcessNa`