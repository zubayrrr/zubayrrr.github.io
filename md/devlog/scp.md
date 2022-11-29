---
created: '2022-03-23T00:00:00.000Z'
desc: ''
id: wosij89dfykieaipt38kees
title: scp
updated: 1653572345276
---
   
Topics::  [linux](../topics/linux.md), [networking](../topics/networking.md)   
   
   
---   
   
`scp` stands for Secure Copy, it allows securely copy files and directories between two hosts, using [ssh](../devlog/ssh.md). It is part of the [OpenSSH](/not_created.md) client package.   
   
## Local to remote   
   
```bash
scp -P 22 file.txt user@hostip:~
```
   
   
```bash
# with specific name
scp -P 22 file.txt user@hostip:~/scp-copied-file.txt
```
   
   
```bash
# to copy a dir use -r for recursive
scp -r -P 22 dirName/ user@hostip:~
```
   
   
```bash
# -p to preserve modification and access time
scp -rp -P 22 dirName/ user@hostip:~
```
   
   
   
- The user must’ve read permissions on the target directory   
   
## Remote to local   
   
```bash
scp user@hostip:/etc/passwd /home/user/Desktop/

# use -r to copy a dir recursively
scp -r user@hostip:~/Desktop /home/user/Desktop
```
   
   
## Remote to remote   
   
```bash
scp user1@IP1:/path_to_source user2@IP2:/path_to_destination
```
   
   
See also: [sftp](../devlog/sftp.md), [FileZilla](/not_created.md), [WinSCP](/not_created.md)