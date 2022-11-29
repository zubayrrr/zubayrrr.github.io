---
created: 20211026071316364
desc: ''
id: u5zkj2qyv4h96h1j83dzgz7
title: /etc/passwd
updated: 1652815757246
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Contains basic information about each user account on the system.   
- `less /etc/passwd`   
- Each line of the file represents a single account   
  - Type, normal or system user   
  - There are seven fields on each line   
- Fields   
   
<!-- end list -->   
   
1.  User's login   
2.  `X` during Unix days it used to contain an encrypted password but these days it represents that a password has been assigned but is stored inside `/etc/shadow`, if this field is blank the user doesn't need to enter a password to login   
3.  User ID - a positive integer assigned to the user followed by:   
4.  Group ID   
5.  Comment, sometimes left blank   
6.  User's home dir   
7.  Default shell, usually set to `/bin/bash` if you see `/usr/sbin/nologin` or `/bin/false` it means its a system user. In Linux every process or service should be run a specific user and its recommended it should never be root, for security reasons. To have such a user that can never login, you set it's shell as `/usr/sbin/nologin` or `/bin/false`   
   
See also: [useradd](../devlog/useradd.md), [groups](../devlog/groups.md), [usermod](../devlog/usermod.md), [userdel](../devlog/userdel.md)