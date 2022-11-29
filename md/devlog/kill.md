---
created: 20211028132557816
desc: ''
id: 5fvsvimnn03ahdf59htc6es
title: kill
updated: 1653305592258
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`kill` is used to terminate a process.   
   
It sends a [signal](../devlog/signal.md)to a [process](../devlog/process.md) or a group of processes causing them to act according to the signal.   
   
When the signal is not specified its default is: 15 or [SIGTERM](../devlog/sigterm.md)   
   
`kill -l` to list all available signals: [[SIGHUP],[SIGKILL](../devlog/sigkill.md) etc   
   
Besides `kill`, [killall](../devlog/killall.md) and [pkill](../devlog/pkill.md) can also be used to send signals to processes.