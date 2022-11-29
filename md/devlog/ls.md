---
created: 20211017145226690
desc: ''
id: 5fqo87mub8wr9a7qpy7sxtv
title: ls
updated: 1653437932993
---
   
   
- `~` - tilda symbolizes the current user's `Home` directory   
- `ls` command prints out content of the current working directory(See also: [pwd](../devlog/pwd.md))   
- `ls -d $PWD/*` command to display the absolute path names of all files or directories in the current directory.   
- To list contents of a specific directory `ls path`   
- `ls -1 path` to list out all the content in one column   
- You can do: `ls -F` to filter out the directories   
- To get info about the directory itself(as opposed to info about the contents of the dir): `ls -d path`   
- To get details about directories in longform, use: `ls -l`   
- You can combine options too: `ls -lha`, where `-a` is for hidden dirs   
- You can use the flag `-S` to sort by size.   
- Sort by file type(extension): `ls -l -X path`   
- Use `ls --hide=*.extensionName path` to omit files with a certain extension   
- `ls -lR` to list [recursive](/not_created.md)ly   
- An [Aliases](../devlog/aliases.md) can be set for `ls` to use `ls --color=auto` which determines the colors of the file names listed, such as blue for dirs, cyan for [symlink](../devlog/symlink.md)s etc.   
   
   
---   
   
   
- Reading the results of `ls -lh` where `-l` stands for longform and `h` stands for human readable file size   
- For example:   
   
`drwxr-xr-x 3 kira kira 4.0K Sep 3 17:01 Applications`   
   
   
- `d` signifies that its a directory( `-` means a normal file, `l` indicates a [symlink](../devlog/symlink.md)).   
- The 9 characters after file type (d, l, -), are the permissions for the owner, group owner and the others, example:   
- `rwx` signifies file permissions for the user and group `kira`.   
- `x` execute, `r` read, `w` write   
- `3` is the number of hardlinks   
- The first `kira` is the user, the second `kira` is the group, `4.0K` is the size (in kilobytes), last modified date and the actual name of the file (in this case `Applications`)   
   
   
---   
   
### ls -lh vs [du](../devlog/du.md) -sh   
   
   
- `ls -lh` doesn't return the true size of the file/dir, it returns the size as reported by the [inode](../devlog/inode.md) structure.   
- Use `du -sh path` to return the true size of the file/dir