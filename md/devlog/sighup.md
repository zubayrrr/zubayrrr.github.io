---
created: 20211028133927950
desc: ''
id: my6skj9hdj9nn7unxwbcudb
title: SIGHUP
updated: 1653318304097
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The SIGHUP signal is sent to a process when its controlling terminal is closed. It was originally designed to notify the process of a serial line drop (a hangup). In modern systems, this signal usually means that the controlling pseudo or virtual terminal has been closed. Many daemons will reload their configuration files and reopen their logfiles instead of exiting when receiving this signal. [nohup](/not_created.md) is a command to make a command ignore the [signal](../devlog/signal.md).   
   
> —via [POSIX signals](https://dsa.cs.tsinghua.edu.cn/oj/static/unix_signal.html)   
   
### Example   
   
Servers read their configuration file only once on their boot up to make them reload, we can use SIGHUP signal, in this example, we'll use [ssh](../devlog/ssh.md) [daemon](../devlog/daemon.md)   
   
   
- `sudo systemctl status ssh`   
- `tail -f /var/log/auth.log/`   
- The [PID](../devlog/pid.md) of a server, is typically located inside `/var/run` dir   
  - `ssh.pid` will be the name of the file that is storing the [PID](../devlog/pid.md) in our case   
- `cat /var/run/ssh.pid` or `pgrep -l sshd` using [pgrep](../devlog/pgrep.md)   
- `sudo kill -1 processID` or `sudo kill -1 $(cat /var/run/sshd.pid)`   
  - The daemon should reload