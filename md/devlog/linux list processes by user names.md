---
created: 20211026115302020
desc: ''
id: ttcawyj21hc9ioq2zc52fdb
tags:
- tidbits
title: Linux list processes by user names
updated: 1652622337784
---
   
Linux list processes by user names   
The procedure to view process created by the specific user in Linux is as follows:   
   
Open the terminal window or app   
   
   
- To see only the processes owned by a specific user on Linux run: `ps -u {USERNAME}`   
- Search for a Linux process by name run: `pgrep -u {USERNAME} {processName}`   
- Another option to list processes by name is to run either `top -U {userName}` or `htop -u {userName}` commands   
   
See all process crated by user named tom:   
`ps -u tom` or `ps -U tom`   
   
> —via [Linux list processes by user names (EUID and RUID) - nixCraft](https://www.cyberciti.biz/faq/linux-list-processes-by-user-names-euid-and-ruid/)