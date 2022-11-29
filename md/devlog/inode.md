---
created: 20211024101739300
desc: ''
id: dwnum4w9cbqdhsbd1y7but3
title: inode
updated: 1653437909475
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Each inode is uniquely identified by an integer number called inode number (`ls -i`).   
- inode structure has pointers to the data blocks where the file contents are saved.   
- The file name doesn't belong to the file strcture, its just a string(a pointer) between file strcture, the connection happens with the data structure through the directory that contains the file. This association between the file structure and file name is called a [hard link](../devlog/hard%20link.md)   
- A file can have multiple names and can be accessed through same directory or different ones.   
- `ln a.txt b.txt` using the `ln` command you can create a new `hard link` to one file, essentially giving it multiple names. The information on the disk is saved only once both files(names) point to the same data. If you edit one the other will be effected (obviously).   
- `ln b.txt /path-to-dir/c.txt` - `hard link` in a different dir.   
- `rm a.txt` will only depreciate the `hard link` associated with it in the inode structure, both `b.txt` and `c.txt` still exist and the space will only be availble once the `hard link` is `0` for those files.   
- To find the other [hard link](../devlog/hard%20link.md)s using inode number `find . -inum inodeNumber`   
- A hard link cannot cross the file system boundaries, you cannot make a hard link for a file in a different partition or a disk.   
- `ls -la /etc/ | less`   
- `find /usr/ -type f -links +1` files with hard links greater than 1   
   
See also: [symlink](../devlog/symlink.md)