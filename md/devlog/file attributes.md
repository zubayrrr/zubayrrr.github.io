---
created: 20211027181819556
desc: ''
id: qfc3k99hj61yzdpez1zbfg4
title: File Attributes
updated: 1653683833093
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
### File Attributes   
   
   
- A part from permissions Linux also has advance access control features such as [ACL](/not_created.md)s and attributes.   
- The attributes define the properties of the files, they depend on the underlying file system such as [ext4](/not_created.md) where the attribute data must be stored along with other control structures.   
- Each file attribute can have one of the two states: `set` or `clear`   
- Attributes is separate from other metadata such as file system permissions, owners, groups, timestamps and so on.   
- [ls](../devlog/ls.md) doesn't display the file attributes, use [lsattr](../devlog/lsattr.md) for that and to change attributes use [chattr](../devlog/chattr.md)