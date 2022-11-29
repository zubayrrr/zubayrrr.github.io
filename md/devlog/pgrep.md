---
created: 20211028101903224
desc: ''
id: 2x54d3zk1jvphjt0102em8k
title: pgrep
updated: 1653305443294
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`pgrep` looks through the currently running processes and lists the process IDs which match the selection criteria to stdout(to the terminal). All the criteria have to match.   
   
For example   
   
`pgrep -u root sshd` will only list the processes called sshd AND owned by root. On the other hand, `pgrep -u root,daemon` will list the processes owned by root OR daemon.   
   
   
- `pgrep -l sshd` to get both [process](../devlog/process.md) IDs and names   
- `pgrep -l cups` its not looking for the whole name but also partial names   
   
See also: [pstree](../devlog/pstree.md)