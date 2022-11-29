---
created: '2022-05-12T00:00:00.000Z'
desc: ''
id: c2ygluwiufvobtlc1i4pf3x
title: lsof
updated: 1657745996226
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Display list of files that are open by a process   
   
```
lsof

# specific options

# filter by user

lsof -u userName
sudo lsof -u root

# use ^ for negation

sudo lsof -u ^root

# filter by process

sudo lsof -c ngnix
```
   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
Almost all Linux users know the ls command.   
   
Not many Linux users know about lsof command.   
   
→ls command lists file   
   
→lsof command lists opened file (by process and users)   
   
This thread will help you learn the lsof Linux command 👇🧵   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081622293516288)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
If you use lsof command without any options and arguments   
   
→lsof   
   
it will list all opened files by all the processes in the system.   
   
The output is likely to be huge and this is why you should use it wisely and in combination of other commands and options. [pic.twitter.com/fIb4Awghyn](https://twitter.com/LinuxHandbook/status/1547081626420760576/photo/1)   
   
![3_1547081616044048384](../assets/3_1547081616044048384.jpg)   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081626420760576)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
List all the processes that have opened a certain file   
   
→lsof path_to_file   
   
You may have to use sudo or be root for better results.   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081630933712896)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
You can list all the files opened by a certain user in Linux:   
   
→lsof -u user1   
   
Or by multiple users:   
   
→lsof -u user1 user2   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081635094470656)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
If you are wondering which of the files have been opened in a certain directory,   
   
you can use lsof command with +D option.   
   
→lsof +D path_to_directory   
   
The search is recursive. It lists all the opened files in the mentioned directory and all of its sub-directories.   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081639091634178)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
If you know the process id, you can use the -p option of the lsof command to find the files opened by a process:   
   
→lsof -p PID   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081643143438337)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
List all files opened by a Linux command:   
   
→lsof -c command   
   
This is specially helpful in debugging. Suppose you want to see what files are used by http daemon, you just need to specify the command name (httpd in our example).   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081647190904832)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
You can combine options like user and command and a process using the –a option.   
   
→lsof -a -u user_name -c command_name   
   
Think of it as the AND operator. This gives you an additional filter while trying to narrow down your search.   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081651288768513)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
You can also use lsof command to find open ports in Linux or for finding which process is using a port.   
   
List all open ports and their processes:   
   
→lsof -i   
   
To find which process is using a specific port:   
   
→lsof -i :portnumber   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081655369736193)   
   
   
---   
   
![LinuxHandbook](../assets/LinuxHandbook-1023073045781590019.jpg)   
Linux Handbook ([@LinuxHandbook](https://twitter.com/LinuxHandbook))   
   
You can use the negation operator to exclude a user or process while using lsof command.   
   
For example, if you want to list all the files opened by a user other than root, use:   
   
→lsof -u ^root   
   
[Tweet link](https://twitter.com/LinuxHandbook/status/1547081659467571201)