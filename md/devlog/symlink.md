---
caption: Symbolic link
created: 20211017125709604
desc: ''
id: ztyk0cbpfcvz4h2czvm3tp4
title: symlink
updated: 1653437927539
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- They're similar to shortcuts in Windows but work differently from [hard link](../devlog/hard%20link.md)s   
- It is a special file type that points to or contains a reference to another file or directory.   
- [hard link](../devlog/hard%20link.md) references the files's [inode](../devlog/inode.md), symlink references another file.   
- If you delete the file that is being pointed by the symlink, the symlink breaks and becomes useless.   
- symlink has its own [inode](../devlog/inode.md) structure   
- symlink only contains the path to the original directory not its contents.   
- Permissions of symlink doesn't matter since the permission of the target file are checked.   
   
### Examples   
   
   
- `ln -s /etc/passwd ./pswd` -s to create a symlink, check with `ls -l pswd`   
- `ps aux > processes.txt`   
  - To create a [hard link](../devlog/hard%20link.md): `ln processes.txt p.txt`   
  - To create a symlink: `ln -s processes.txt symlink_p.txt`   
  - To check `ls -li`   
  - If we were to change the location of `processes.txt`, `p.txt` will not be effected but `symlink_p.txt` will be broken.   
- You can create a symlink to a dir(altough you cannot create a [hard link](../devlog/hard%20link.md) to a dir)   
  - `ln -s /etc/ symlink_etc`