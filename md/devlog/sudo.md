---
created: 20211026112255790
desc: ''
id: jqyxvlopjrxj27o648plyk9
title: sudo
updated: 1653683844832
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
> sudo (Super User DO) command in Linux is generally used as a prefix of some command that only superuser are allowed to run. If you prefix “sudo” with any command, it will run that command with elevated privileges or in other words allow a user with proper permissions to execute a command as another user, such as the superuser. This is the equivalent of “run as administrator” option in Windows. The option of sudo lets us have multiple administrators.   
>   
> These users who can use the sudo command need to have an entry in the sudoers file located at “/etc/sudoers”. Remember that to edit or view the sudoers file you have to use sudo command. To edit the sudoers file it is recommended to use “visudo” command.    
> By default, sudo requires that users authenticate themselves with a password which is the user’s password, not the root password itself.   
>   
> —via [sudo command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/sudo-command-in-linux-with-examples/)   
   
   
- In CentOS sudo is `wheel`   
   
### Creating Admin Users   
   
   
- A user has to be added to the [sudo](../devlog/sudo.md) [group](/not_created.md) or the `sudoer file` inorder for them to use `sudo` privileges, [usermod](../devlog/usermod.md) can be used to achieve this.   
  - `sudo usermod -aG sudo james`