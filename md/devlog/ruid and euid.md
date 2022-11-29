---
created: 20211026114606684
desc: ''
id: 85wfonu33weha94nf7wyxcc
title: RUID and EUID
updated: 1653318304089
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
A Linux process is nothing but running instance of a program. For example, when you start Firefox to browse Internet, you can create a new process. In Linux, each process is given a unique number called as a process identification ([PID](../devlog/pid.md)). Linux kernel makes sure that each process gets a unique PID. /sbin/[init](/not_created.md) or /lib/systemd/[systemd](../devlog/systemd.md) on modern Linux distros always has a PID of 1 because it is eternally the first process on the Linux based system. The `ps` command used to list the currently running processes and their PIDs on Linux.   
   
Linux list processes by user names   
The procedure to view process created by the specific user in Linux is as follows:   
   
Open the terminal window or app   
   
   
- To see only the processes owned by a specific user on Linux run: `ps -u {USERNAME}`   
- Search for a Linux process by name run: `pgrep -u {USERNAME} {processName}`   
- Another option to list processes by name is to run either `top -U {userName}` or `htop -u {userName}` commands   
   
See all process crated by user named tom:   
`ps -u tom` or `ps -U tom`   
   
> —via [Linux list processes by user names (EUID and RUID) - nixCraft](https://www.cyberciti.biz/faq/linux-list-processes-by-user-names-euid-and-ruid/)   
   
EUID is the Effective User ID. The effective user ID describes the user whose file access permissions are used by the process. RUID is the Real User ID. The real user ID identifies the user who created the process. So:   
   
   
- `-u tom` : Show all processes by RUID   
- `-U tom` : Display all processes by EUID   
   
> —via [Linux list processes by user names (EUID and RUID) - nixCraft](https://www.cyberciti.biz/faq/linux-list-processes-by-user-names-euid-and-ruid/)   
   
Essentially:   
   
EUID - The current user in the shell that executes the command   
RUID - The user who initially logs in and never changes   
   
## User Account Monitoring   
   
### [whoami](#whoami)   
   
   
- Prints out the [RUID and EUID](../devlog/ruid%20and%20euid.md), the username of the current user when this command is invoked.   
- It is similar as running the [id](../devlog/id.md) command with the options `-un`.   
   
### [who](#who)   
   
   
- It displays the [RUID and EUID](../devlog/ruid%20and%20euid.md), the user that initially logged in(the current shell).   
- `who` parses and displays the contents of the file `/var/run/utmp`, that logs the current users on the system.   
- `/var/log/wtmp` - its kinda like history for the `/var/run/utmp` file, it maintains the logs for all the logged in users and logged out users (in the past)   
- `who -H` -H Prints a line of column headings.   
- `who -aH` a for –all   
- `w` command provides list of users that are logged in, what current processes are they running   
  - `load average` value should be below `1` or else theres a problem   
  - [uptime](/not_created.md) command also provides the same info   
   
### [id](../devlog/id.md)   
   
   
- Prints [RUID and EUID](../devlog/ruid%20and%20euid.md) and its [groups](../devlog/groups.md)   
   
### [last](#last)   
   
`last` command in Linux is used to display the list of all the users logged in and out since the file `/var/log/wtmp` was created. One or more usernames can be given as an argument to display their login in (and out) time and their host-name.   
   
> —via [last command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/last-command-in-linux-with-examples/)   
   
   
- Records are printed in reverse time order, starting from more recent one.   
- `last userName` to find info about a specific user.