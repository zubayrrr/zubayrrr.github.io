---
created: 20211016133625680
desc: ''
id: ktm0z46nm4ur05mdk0nesij
title: passwd
updated: 1653318765360
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
passwd command in Linux is used to change the user account passwords. The root user reserves the privilege to change the password for any user on the system, while a normal user can only change the account password for his or her own account.   
   
### Syntax:   
   
`passwd [options] [username]`   
   
### Note:   
   
[sudo](../devlog/sudo.md) can be used to invoke root privileges by normal users, and can change the password for root itself. This is particularly helpful when a user is member of admin group (holds a position in sudoers list (/etc/sudoers) and can use commands with sudo) and the root password is not set, which is case with many common distributions of linux.   
   
`sudo passwd root`   
   
> —via [passwd command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/passwd-command-in-linux-with-examples/)