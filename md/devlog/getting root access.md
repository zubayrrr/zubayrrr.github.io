---
created: 20211016131145910
desc: ''
id: n7z6kcxrme63oo11wv760w6
title: Getting root Access
updated: 1653318782910
---
   
   
- on Linux there are 2 main categories of users:   
  - Non-privileged users - have no special rights on the system   
  - The root user (superuser or the administrator)   
- root privileges are the powers taht the root account has on the system. the root account is the most privileged on the system and has absolute power over it.   
- Only one root exists on any Linux system.   
- It is not recommend to use root for ordinary tasks. When root permissions are needed you simply become root only to performt hat particular administrative task.   
   
   
---   
   
   
- Become root temporarily(for as long as the terminal session is open):     
  `sudo su` will prompt user to enter their password (NOT the root password), you also do that same using `sudo -i`   
   
- [sudo](../devlog/sudo.md) stands for "substitute user do" and [su](/not_created.md) stands for "substitute user".   
- `sudo` will only let you use `su` if you're part of the `group sudo` (`group wheel` on CentOS).   
- Run the `id` command to check what user you're currently logged in as.   
   
   
---   
   
   
- To login in to the root environment, `sudo su -`, the current working directory will be `/root`.   
- root user prompt ends in `#` as compared to other users whose prompt ends in `$`.   
   
   
---   
   
   
- To enter a command as root user without changing user, just append `sudo` before the command you want to enter (again, this will only work if the user is part of the `group sudo`).   
- `sudo` is cached in the terminal for 5 mins from the time password was entered.   
- By running `sudo -v` the user can add 5 more mins to the cached credentials without running a command.   
- To invalidated cached credentials, run `sudo -k`   
   
   
---   
   
   
- In certain distros (such as Ubuntu), root password is not defined by default(you cannot login as root at all(using `su` command) unless you set a password for the root user).   
- To set password for the root user: `sudo passwd root`   
- To temporarily logging in as root: `su` and enter the root user's password.   
   
See also: [passwd](../devlog/passwd.md)