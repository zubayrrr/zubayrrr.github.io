---
created: '2021-10-26T00:00:00.000Z'
desc: ''
id: a0uv6ed8j3idxwfyhn8kj8l
title: User Account Monitoring
updated: 1653307887187
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
## User Account Monitoring   
   
### [whoami](../devlog/whoami.md)   
   
   
- Prints out the [RUID and EUID](../devlog/ruid%20and%20euid.md), the username of the current user when this command is invoked.   
- It is similar as running the [id](../devlog/id.md) command with the options `-un`.   
   
### [who](../devlog/who.md)   
   
   
- It displays the [RUID](../devlog/ruid%20and%20euid.md), the user that initially logged in(the current shell).   
- `who` parses and displays the contents of the file `/var/run/utmp`, that logs the current users on the system.   
- `/var/log/wtmp` - its kinda like history for the `/var/run/utmp` file, it maintains the logs for all the logged in users and logged out users (in the past)   
- `who -H` -H Prints a line of column headings.   
- `who -aH` a for –all   
- `w` command provides list of users that are logged in, what current processes are they running   
  - `load average` value should be below `1` or else theres a problem   
  - [uptime](/not_created.md) command also provides the same info   
   
### [id](../devlog/id.md)   
   
   
- Prints [EUID](../devlog/ruid%20and%20euid.md) and its [groups](../devlog/groups.md)   
   
### [last](../devlog/last.md)   
   
`last` command in Linux is used to display the list of all the users logged in and out since the file `/var/log/wtmp` was created. One or more usernames can be given as an argument to display their login in (and out) time and their host-name.   
   
> —via [last command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/last-command-in-linux-with-examples/)   
   
   
- Records are printed in reverse time order, starting from more recent one.   
- `last userName` to find info about a specific user.