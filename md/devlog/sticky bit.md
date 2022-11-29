---
created: 20211027154626236
desc: ''
id: zgy59mvs3o3ip3431luuj11
title: Sticky Bit
updated: 1652815757388
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
### special Permission - Sticky Bit   
   
   
- The Sticky Bit is applied to directories   
- A user may only delete files that he owns or for which he has explicit write permission granted, even when he has write access to the directory   
- The sticky bit allows you to create a directory that everyone can use as a shared file storage. The files are protected because, no one can delete anyone else's files.   
- Absolute Mode: `chmod 1xxx directory`   
- Relative Mode: `chmod o+t directory`   
- `ls -ld /temp/`   
  - `drwxrwxrwxt 2 root root 4096 iul 14 13:45 /temp/`   
   
For example:   
   
   
- `sudo su`   
- `mkdir /temp`   
- `chmod 777 /temp`   
   
A nonprivileged user(inside `/temp`):   
   
   
- `touch file1 file2`   
- `chmod 600 file*`   
   
Now as per the parent directory's permissions, any user should be able to delete the files that the nonprivileged user created. To mitigate this issue   
   
   
- `sudo su`   
- `chmod 1777 /temp` or `chmod o+t /temp`   
   
To verify `ls -ld /temp` or `stat /temp` you should be able to find a `t` appended to the existing permissions. If you see an uppercase `T` instead, it means the dir doesn't have [x] executable permissions(uncommon).   
   
`/var/tmp` and `/tmp/` are also dirs with Sticky Bit set.