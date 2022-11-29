---
created: '2022-05-14T00:00:00.000Z'
desc: ''
id: ixi78tg04g5oavzuk4a8plt
title: umount
updated: 1653306004747
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`umount` Un[mount](../devlog/mount.md)s a previously mounted file system, directory, or file.   
   
```
sudo umount /dev/sdb
```
   
   
You cannot use the **umount** command on a device in use. A device is in use if any file is open for any reason or if a user's current directory is on that device.   
To overcome this use the `-l` (lazy) option. This causes `umount` to wait until the file system is able to be safely unmounted.   
   
```
sudo umount -l /dev/sdb
```
