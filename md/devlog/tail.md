---
created: 20211017104731584
desc: ''
id: ixrpyxbv543ssnlpo6dm5q3
title: tail
updated: 1652815757628
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
It is the complementary of [head](../devlog/head.md) command.The tail command, as the name implies, print the last N number of data of the given input. By default it prints the last 10 lines of the specified files. If more than one file name is provided then data from each file is precedes by its file name.   
   
> —via [Tail command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/tail-command-linux-examples/)   
   
   
- Syntax:   
  - `tail path-to-file`   
  - `tail -n number path-to-file` to view custom number of lines   
  - `tail -n +20 path-to-file` to views lines from the line \# 20   
- `tail` is most commonly used to watch log files as they're updated   
  - `tail -f path-to-file` to watch the file in real time as it gets updated   
- Example:   
  - `tail -n 15 -f /var/log/auth.log`