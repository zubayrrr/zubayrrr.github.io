---
created: 20211028201906976
desc: ''
id: 3dz4uwat5h6zuz2tt5xluoe
title: foreground process
updated: 1653305865781
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Foreground processes are started by the user and not by the system services and while they're running, the user cannot start another from the same terminal. By default every [process](../devlog/process.md) you start runs in the foreground. It gets its input from the keyboard and sends output through the terminal. Simulate this using the `sleep` command, `sleep 15` will run in foreground for 15 seconds.   
   
You can suspend processes running in the foreground anytime by using `Ctrl + Z`, the process will not be discarded from the RAM or terminated, it was simply temporarily stopped and can be viewed using [jobs](../devlog/jobs.md) command when ran from the same shell that started the foreground process.   
   
You can resume is anytime using [fg](../devlog/fg.md) or [bg](../devlog/bg.md)   
   
   
- `bg %JobID` resumes it in the background   
- `fg %JobID` resumes it in the foreground