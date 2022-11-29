---
created: 20211027150229930
desc: ''
id: 29n92e4t22kpncwz11elghh
title: SUID
updated: 1653683859061
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
### Special Permission - [suid](../devlog/suid.md)   
   
   
- **When an execuatable file with [suid](../devlog/suid.md) is executed then the resulting process will have the permissions of the owner of the command, not the permissions of the user who executes the command**.   
- Sometimes it is necessary for a system to temporarily treat a user as root which is where [suid](../devlog/suid.md) comes into play.   
  - [passwd](../devlog/passwd.md) command has SUID set by default so that even nonpriviledged users can change their password.   
- Absolute Mode: `chmod 4xxx file`   
- Relative Mode: `chmod u+s file`   
- `ls -l /usr/bin/passwd`   
  - `-rwsr-xr-x 1 root root 68208 apr 16 15:36` /usr/bin/passwd   
   
For example:   
   
`cat` will only be able to read a file if the user has the permissions to read the file.   
   
`ls -l /usr/bin/cat` the owner of the executable is `root` but it'll be run as per the privileges of the user that invokes the command.   
   
In case of `/etc/shadow` file, `cat` will not be able to read the contents because it doesn't yet have the [suid](../devlog/suid.md) `s` set for it, so its not able to inherit the permissions of the `root`, even though `root` is the owner of the command `cat` but since [suid](../devlog/suid.md) is not set, it is inherting the permissions of the nonprivileged user.   
   
If there is a `0` before the numeric value for "Access" when you run [stat](../archive/STAT.md) on a file, it means there are no special permissions set for that file.   
   
### Setting up SUID   
   
`sudo chmod 4755 /usr/bin/cat` using [chmod](../devlog/chmod.md) setting the [suid](../devlog/suid.md) and checking with `ls -l /usr/bin/cat` will return `-rwsr-xr-x` with /usr/bin/cat in red(or different) color.   
   
If you check with [stat](../archive/STAT.md) command you'll find "Access" with the value: `4755`   
   
Sometimes you'll find an uppercase `S` instead of a lowercase `s` denoting that there are no `x` executable permissions for that file.   
   
#### SUID with symbolic mode   
   
`sudo chmod u+s /usr/bin/cat`   
   
### Finding all the commands with the SUID set   
   
`find /usr/bin -perm -4000` [find](../devlog/find.md)