---
created: 20211027120546276
desc: ''
id: 6vzwh1eaj567nroqwy1uf5s
title: The Effect of Permissions on Directories
updated: 1653437919624
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Permissions for files have a different effect as permissions for directories in Linux.   
   
To test, create a dir with only read permissions \*`chmod 400 folder`   
   
You can only run `ls -ld` but you cannot go inside the dir make any changes, add files or delete files from that dir, you cannot even `ls -l` since that would mean it would look for the file types, permissions, owners etc(content metadata cannot be read), `ls --color=auto` (often [Aliases](../devlog/aliases.md) as `ls`) is also not allowed as it would try to recogize the file types.   
   
You can however, rename the `folder` dir   
   
Adding, `r`,`w` permissions   
   
   
- `chmod 600 folder`   
   
Even though write permissions have been added to `folder` you'll still not be able to perform the actions discussed above. If `x` execute permissions are not set the write permissions don't really do anything.   
   
The `x` execute permissions give access to the contents of the directory.   
   
   
- `chmod 700 folder`   
   
Now you'll be able everything on that directory,   
   
   
---   
   
### The permissions of the parent directory are more important than the file permissions.   
   
To test, create a file inside the `folder` dir and remove all permissions for that file and try to delete it.   
   
   
- `touch folder/file.txt`   
- `chmod 000 folder/file.txt`   
- `rm folder/file.txt`