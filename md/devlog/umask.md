---
created: 20211027155934704
desc: ''
id: vgmdtjl7emz7npfah8ttgsx
title: umask
updated: 1653437420500
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
When user create a file or directory under Linux or UNIX, they create it with a default set of permissions. In most case the system defaults may be open or relaxed for file sharing purpose. For example, if a text file has 666 permissions, it grants read and write permission to everyone. Similarly a directory with 777 permissions, grants read, write, and execute permission to everyone.   
   
### Default umask Value   
   
The user file-creation mode mask (umask) is use to determine the file permission for newly created files. It can be used to control the default file permission for new files. It is a four-digit octal number. A umask can be set or expressed using:   
   
   
- Symbolic values   
- Octal values   
   
> —via [What is Umask and How To Setup Default umask Under Linux? - nixCraft](https://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html)   
   
It is used by [mkdir](../devlog/mkdir.md), [touch](../devlog/touch.md) and other commands that create new files, dirs.   
   
The default permissions with which news files/dirs are created are determined by `umask`.   
   
### Default permissions   
   
   
- `0666` for files   
- `0777` for directories   
   
umask value - default permissions = current permission   
   
run `umask` to get default umask value   
   
0777 - 0002 = 0775 for dirs   
0666 - 0002 = 0664 for files   
   
### Working with `umask`   
   
`umask umaskNumber`   
   
   
- The permissions of the existing files are not effected, only the files created after the changing of the `umask` value will have effect.   
- The `umask` value only lasts as long as the terminal instance is open.   
- To make this change persist add it to the user's `.bashrc` file.   
   
<span class="underline">It is however uncommon to change default</span> `umask`<span class="underline">'s value</span>