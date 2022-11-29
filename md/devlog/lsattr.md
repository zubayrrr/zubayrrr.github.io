---
created: 20211027181214604
desc: ''
id: pdd1ljoj7m3l5k35ixyh4ax
title: lsattr
updated: 1653437835252
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`lsattr` is used to display the file attributes for the subdirectories of the current directory.   
   
`-` indicates attribute is cleared and alphabets represent different attributes such as:   
   
   
- The `e` attribute indicates that the file is using extents for mapping the blocks on disk. It may not be removed using [chattr](../devlog/chattr.md).   
- The `I` attribute is used by the htree code to indicate that a directory is being indexed using hashed trees. It may not be set or reset using [chattr](../devlog/chattr.md), although it can be displayed by `lsattr`.   
   
`lsattr -R dirName` to list attributes recursively(of the subdirectories)   
   
For more: man [chattr](../devlog/chattr.md)