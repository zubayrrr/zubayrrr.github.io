---
created: 20211026104643588
desc: ''
id: 1f4l7a9xnqhhmf0a7cnkhi1
title: groupadd
updated: 1652815757599
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`groupadd` command is used to create a new user [groups](../devlog/groups.md).   
   
Syntax:   
   
`sudo groupadd [option] group_name `   
   
   
- `sudo groupadd engineering` create a new group   
- `tail -3 /etc/group` or `cat /etc/group` - check last 3 groups or all groups inside `/etc/group`   
- Adding users to the group can be acheived using [useradd](../devlog/useradd.md), note that users can only be added to groups that have already been created using `groupadd`   
- [groupmod](../devlog/groupmod.md) can be used to make changes to the group name, [groupdel](../devlog/groupdel.md) to delete a group