---
created: 20211027142734364
desc: ''
id: wi4hrouup889hj4e5qxj9kx
title: chown
updated: 1652815757258
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The `chown` command allows you to change the user and/or group ownership of a given file, directory, or symbolic link. `chown` is root only command.   
   
   
- It is not possible to disown a file   
- Even the owner cannot change the ownership of the file, only root can   
- The numeric user ID can also be used instead of the username(`cat /etc/passwd`)   
   
### Examples   
   
`sudo chown userName fileName.txt`   
   
`sudo chown userName file1.txt file2.txt folder`   
   
`sudo chown +userID file.txt` to avoid mistransfer using user ID prefix the userID with a `+` plus sign   
   
`sudo chown userName:groupName file.txt` to change both owner and group, you can also use a `.` to separate user and group, `userName.groupName`   
   
To only change the group of a file, use `chgrp` or `sudo chown :groupName file.txt`   
   
Use `-R` to recursively change ownership of files inside a dir   
   
`sudo chown -R userName:groupName folder`