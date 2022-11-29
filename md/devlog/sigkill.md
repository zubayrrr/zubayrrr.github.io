---
created: 20211028135238396
desc: ''
id: odobz2lkl658ukcl7h241iu
title: SIGKILL
updated: 1653305505908
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The SIGKILL [signal](../devlog/signal.md)is sent to a [process](../devlog/process.md) to cause it to terminate immediately ([kill](../devlog/kill.md)). In contrast to [SIGTERM](../devlog/sigterm.md) and [SIGINT](/not_created.md), this signal cannot be caught or ignored, and the receiving process cannot perform any clean-up upon receiving this signal.   
   
> —via [POSIX signals](https://dsa.cs.tsinghua.edu.cn/oj/static/unix_signal.html)   
   
   
- Also known as `hard kill`