---
created: 20211027181733650
desc: ''
id: zm7piwt6fbobsmqwd1yt057
title: chattr
updated: 1653683833112
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`chattr` is used to change [File Attributes](../devlog/file%20attributes.md) on a Linux file system.   
   
The operator `+` causes the selected attributes to be added to the existing attributes of the files; `-` causes them to be removed; and `=` causes them to be the only attributes that the files have. (via `man chattr`)   
   
The letters 'acdeijstuADST' select the new attributes for the files:   
   
   
- append only (a)   
- compressed (c)   
- no dump (d)   
- extent format (e)   
- immutable (i)   
- data journalling (j)   
- secure deletion (s)   
- no tail-merging (t)   
- undeletable (u)   
- no [atime](/not_created.md) updates (A)   
- synchronous directory updates (D)   
- synchronous updates (S)   
- top of directory hierarchy (T)   
   
The following attributes are read-only, and may be listed by [lsattr](../devlog/lsattr.md) but not modified by [chattr](../devlog/chattr.md):   
   
   
- huge file (h)   
- compression error (E)   
- indexed directory (I)   
- compression raw access (X)   
- compressed dirty file (Z)   
   
Not all flags are supported or utilized by all file systems; refer to file system-specific man pages such as [btrfs](/not_created.md), [ext4](/not_created.md), and [xfs](/not_created.md) for more file system-specific details.   
   
> —via [chattr(1): change file attribs on file system - Linux man page](https://linux.die.net/man/1/chattr)   
   
### Examples   
   
   
- `sudo chattr +a file.txt` now `file.txt` is append only   
- `sudo chattr +A file.txt` no access time (atime) update (helps save system resources)   
- `sudo chattr +i file.txt` cannot be modified, deleted, no [hard link](../devlog/hard%20link.md), no read, write, change permission. Only the the superuser (root) user has the capability to set or clear this attribute(only then the file can be removed)   
- `sudo chattr -R +i dirName` to set it recursively