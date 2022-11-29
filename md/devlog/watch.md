---
created: 20211022075034540
desc: ''
id: a0bok2ylus32myn03vfo8vr
title: watch
updated: 1652815757415
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- `watch` is used to run any arbitrary command at regular intervals and displays the output of the command on the terminal window.   
- It is useful when you have to execute a command repeatedly and watch the command output change over time. For example, you can use the watch command to monitor the system uptime or disk usage.   
- The watch utility is a part of the procps (or procps-ng) package which is pre-installed on nearly all Linux distributions.   
- You can use `-d` flag to view difference between two successive updates, `-n` option to change the update interval time.   
- Examples:   
  - `watch -n 3 -d ls -l`   
  - `watch date`   
  - `watch ls`   
  - `watch -n 1 -d ifconfig` to keep track of network traffic