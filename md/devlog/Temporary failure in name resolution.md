---
created: 1653986856711
desc: ''
id: 8rs7hg86ukb4trv57uixph6
tags:
- tidbits
title: Temporary failure in name resolution
updated: 1653986916812
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
> if /etc/resolv.conf is a symbolic link, you won't be able to write it. If you want to overwrite the content in the file, remove the file and then create a new fi   
   
1. Remove symbolic link   
   `sudo rm /etc/resolv.conf`   
2. Write to new file. E.g.   
   `sudo echo "nameserver 8.8.8.8" > /etc/resolv.conf`   
   
— via [resolvconf - /etc/resolv.conf" E166: Can't open linked file for writing - Ask Ubuntu](https://askubuntu.com/questions/1071656/etc-resolv-conf-e166-cant-open-linked-file-for-writing)