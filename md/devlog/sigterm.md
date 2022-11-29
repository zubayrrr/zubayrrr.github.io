---
created: 20211028134808284
desc: ''
id: 9b3sbqneahrz434hmpaw5qi
title: SIGTERM
updated: 1653304890694
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The SIGTERM [signal](../devlog/signal.md)is sent to a [process](../devlog/process.md) to request its termination. Unlike the [SIGKILL](../devlog/sigkill.md) signal, it can be caught and interpreted or ignored by the process. This allows the process to perform nice termination releasing resources and saving state if appropriate. [SIGINT](/not_created.md) is nearly identical to SIGTERM.   
   
> —via [POSIX signals](https://dsa.cs.tsinghua.edu.cn/oj/static/unix_signal.html)   
   
   
- The process may stop immediately, it can stop after some day (after cleaning up resources etc) or the process may run indefinitely (ignore), the process decides what it wants to do.   
- It is also called as a `soft kill`   
- Processes that ignore SIGTERM will have to be terminated using [SIGKILL](../devlog/sigkill.md)