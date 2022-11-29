---
created: '2021-10-26T00:00:00.000Z'
desc: ''
id: efnqf3f1g48bzgd64jwx9r9
title: useradd
updated: 1653683844842
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- `useradd` command is used to add new users to the system   
- `sudo useradd ` to create a new user   
  - The new user will be created with the default options as specified in `/etc/default/useradd`   
  - By default, a [group](/not_created.md) with the same name as the new user will be created and assigned   
  - To be able to login as the new user, a password will have to be set: `sudo passwd userName`   
- `useradd` also reads the contents of the file `/etc/login.defs`, which contains options for the `/etc/shadow` such as password expiration policy, ranges of user IDs when creating system and regular users and more.   
   
### Creating a user with options   
   
   
- When a user is created without passing any options, it's home directory is also not created.   
- To create the user's home directory, use `-m` option   
- You can give it a different name or location by passing the `-d` option followed by the path   
- To write a comment use `-c` option followed by the string, typically a short description such as user's full name or a contact info   
- To alot the user a specific shell pass the `-s` followed by the absolute path of the shell. Usually its `/bin/bash`   
- By default the user's primary group is same as the user's name, use the `-g` option to add the user to a different primary group (uncommon)   
- To add the user to secondary group use the `-G` followed by group names, separated by commas (the groups should already exist)   
- lastly the name of the user `james`   
   
`sudo useradd -m -d /home/james -c "C++ Developer james@email.com -s /bin/bash -G sudo,adm,mail james"`   
   
Do not forget to create a password for the newly created user   
   
   
---   
   
   
- If you want to create a temporary user, set an expiration date on which the user account will be disabled.   
   
`sudo useradd -e 2021-12-31 userName`   
   
   
- `chage` command to change expiration date for an existing user.   
  - `sudo chage -l james` `-l` to get age info   
   
   
---   
   
### `useradd` vs `adduser`   
   
   
- `useradd` is a native binary complied in a Linux system   
- `adduser` is just a perl script that uses `useradd` binary as a backend   
  - `adduser` is more interactive and user friendly than `useradd`   
  - commonly found in Ubuntu systems.