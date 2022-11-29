---
created: 20211028080401140
desc: ''
id: 8lrs6sx3o09qlh0s1j7dzoc
title: type
updated: 1652815757549
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- There are two type of commands, executables files on the disk and shell builtin commands.   
- To check if a command is an executable or a shell builtin command, use `type` followed by the command you want to check, example: `type df`, if it returns a path, its an executable and will have a dedicated [Man Pages](../devlog/man%20pages.md).   
- If a command is a shell builtin, such as: `type cd`, it'll return "cd is a shell builtin".   
- `type` is also a shell builtin