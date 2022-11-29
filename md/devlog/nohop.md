---
created: 20211028205052388
desc: ''
id: tubz5rys0brzeqe3c6frkw5
title: nohop
updated: 1653318304105
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
When you close a terminal, logout or disconnect, any processes running in that terminal will be terminated. [[SIGHUP] signal is sent to the process and the process will be killed. This can become an issue if you're running a remote server, executing programs over SSH and if the connection drops, the session will be terminated, all the executed processes will stop, to avoid this issue, use `nohop` command which will make the process ignore all hang up signals.   
   
[Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) will not be available to the user and `nohup.out` file is used as the default file for [stdout](../devlog/stdout.md) and [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md), it is created in the current working directory or if the user doesn't have the right permissions for the current directory, the file will be created in the user's home dir. If the output of the nohup command is redirected to some other file, nohup.out file is not generated.   
   
If a process is started and its parent(bash shell) gets terminated, the process will be adopted by [init](/not_created.md) or [systemd](../devlog/systemd.md) which runs with the [PID](../devlog/pid.md) `1` and are the first process run by the system.   
   
   
- `nohup sleep 123 &` will begin a `sleep` process   
   
Alternatives to nohup are [GNU Screen](https://www.gnu.org/software/screen/) and [tmux](https://github.com/tmux/tmux)