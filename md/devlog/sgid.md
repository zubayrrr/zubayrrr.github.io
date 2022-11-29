---
created: 20211027152328988
desc: ''
id: 51fvmn1jjdv3mqercybkjz9
title: SGID
updated: 1653683878002
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
### Special Permission - [SGID](../devlog/sgid.md)   
   
   
- SGID or Set Group ID   
- SGID is set mainly to directories   
- If you set SGID on directories, all files or directories created inside that directory will be owned by the same group owner of the directory where SGID was configured.   
- This is useful in creating shared directories, which are directories that are writable at the group level.   
- Absolute Mode: `chmod 2xxx directory`   
- Relative Mode: `chmod g+s directory`   
- `ls -ld /programming/`   
  - `drwxrws---2 pr1 programmers 4096 iul 14 13:15 /programming/`   
   
For example:   
   
   
- `sudo su`   
- `groupadd programmers`   
- `useradd -s /bin/bash pr1`   
- `useradd -s /bin/bash pr2`   
- `usermod -aG programmers pr1`   
- `usermod -aG programmers pr2`   
- `mkdir /programming/`   
- `chown pr1:programmers /programming/`   
- `chmod 770 /programming/`   
- `su pr1`   
- `cd /programming/`   
- `touch source1.cpp`   
   
At this point the <span class="underline">group owner of the file is the primary group of the creator</span> and the other users in the `programmers` group will not be able to change the file or work on it, we can give individual permissions to the other users but it can be a security issue.   
   
### Setting up SGID   
   
`chmod 2770 /programming` or `chmod g+s /programming`   
   
Verify with `ls -ld /programming` or `stat /programming`   
   
There will be an additional `s` letter added to the permissions, if there is an uppercase `S` it means there are not execution permissions set for that directory.   
   
   
- `su pr2`   
- `cd /programming`   
- `touch source2.cpp`   
- `mkdir goland python`   
  - Newly created dirs will have similar permissions as the parent directory with the SGID set   
- The group of the newly created files and dirs will be "programmers" and not "pr1"