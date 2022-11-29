---
created: 20211028135602440
desc: ''
id: 1ml1vdkyp8rhohc14leduv0
title: killall
updated: 1653318304099
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`killall` is used for killing any or all running process on the system based on a given name. This command will terminate the processes forcibly when a specified name matches. If no [signal](../devlog/signal.md)name is specified, [SIGTERM](../devlog/sigterm.md) is sent.   
   
It takes name of the process, instead of the [PID](../devlog/pid.md).   
   
`killall` doesn't accept partial names, to [kill](../devlog/kill.md) using partial names, use [pkill](../devlog/pkill.md)   
   
### Example   
   
   
- `killall -15 processName`