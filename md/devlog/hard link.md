---
created: 20211024094337852
desc: ''
id: nomou0zpru770377wzxr6rp
title: hard link
updated: 1653437927541
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- It is an association between an [inode](../devlog/inode.md) structure and a file name in a directory.   
- You cannot create a hard link to a directory.   
- All hard links have some [inode](../devlog/inode.md) structure and [inode](../devlog/inode.md) number   
   
### Example   
   
   
- `ps aux > processes.txt`   
  - To create a [hard link](../devlog/hard%20link.md): `ln processes.txt p.txt`   
  - If we were to change the location of `processes.txt`, `p.txt` will not be effected.