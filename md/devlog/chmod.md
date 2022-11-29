---
created: 20211027101141480
desc: ''
id: 8e78vq83ld131fb43r7xf90
title: chmod
updated: 1653318359121
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- `chmod` is the command used to change the permissions of a file or a directory using either the symbolic or the numeric notation ([Octal Notation](../devlog/octal%20notation.md)).   
- Only the root, or the file's owner can change the file's permissions.   
   
### Syntax:   
   
`chmod [who][OPERATION][permissions] filename`   
   
### `who`   
   
   
- `u` the **user** that owns the file   
- `g` the **group** that the file belongs to   
- `o` the **other** users   
- `a` for **all**   
   
### OPERATION flags   
   
   
- `-` a hyphen means remove the specified permissions   
- `+` the plus sign means add the specified permissions   
- `=` the equals sign means change the current permissions to the specified permissions   
   
The permissions are specified using the letters `r`, `w` and `x`   
   
### Examples   
   
   
- Removing `w` permissions   
  - `chmod u-w file.txt`   
- Adding permissions   
  - `chmod u+rwx file.txt`   
- `chmod -v u-x,g+w,o-rwx file.txt`   
- `chmod ug-r,u+x,o-rwx file.txt`   
- `chmod a+r,a-wx file.txt`   
- `chmod ug=rw,o= file.txt`   
   
### Absolute changing mode   
   
Setting permission for all users, groups, others at the same time   
   
   
- `chmod 644 file.txt`   
- `chmod 777 file.txt`   
- `chmod 400 file.txt`   
- `-R` for recursively assigning permissions   
- `chmod -R 750 dirName.txt` (not recommended since the permissions for files have a different effect as permissions for directories) [The Effect of Permissions on Directories](../devlog/the%20effect%20of%20permissions%20on%20directories.md)   
   
### Inherit permissions from a file   
   
   
- `chmod --reference=refFile.txt file.txt`