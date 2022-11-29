---
created: 20211013140931708
desc: ''
id: hy62pxdr1mo1pamj5uggb2r
title: Navigating the Linux File System
updated: 1653437932991
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
### The [ls](../devlog/ls.md) command   
   
   
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
   
   
---   
   
   
- `cd` command can be used to "change directory" inside the terminal.   
- Just doing `cd` will take you to the `Home` dir of the current user   
- `cd` can be used with absolute path, such as: `cd /home/kira/Downloads`   
- You can also use the tilda symbol instead of statically typing down the current user's name, such as: `cd ~/Downloads` \<— this is same as doing `cd /home/kira/Downloads`   
- You can also use relative path, relative to where you're right now in the terminal(relative to the current directory you're in), such as: `cd Downloads`, because you're already in the `Home` or `~` directory of the current user.   
- Relative path should never start with a forward slash (`/`), although you can use `./` to specify you want to explore the dir relatively.   
- You can check absolute path(which refers to the location of the file on the disk) of the current directory you're at by doing `pwd` in the terminal, which stands for Print Working Directory.   
- To look at hidden files using `ls` you can pass the "all" option `-a`, such as: `ls -a`.   
- You'll find two additional(hidden folders) when you do `ls -a` in the any dir of the current user, named: `.` and `..` .   
- `.` is a shortcut for the current dir, it is useful when you want to refer to the current dir when performing an action.   
- `..` refers to the parent dir or the dir above the current dir, you can keep doing `cd ..` till you eventually reach the `/` dir.   
- While you might be able to see the dirs inside the `/` dir, you'll not be able to `cd` inside the dirs you don't have permissions for such as the `root` dir   
   
   
---   
   
   
- You can press the `Tab` key on your keyboard to autocomplete file/dir/command names.   
- When the autocomplete is not able to guess, you might have to give it an extra letters(from the dir you're trying to navigate to) to follow up on.   
- When you double press `Tab` key, it'll prompt all possible entries for autocompletion.   
- If `Tab` autocomplete isn't working when it should be, theres probably aan error on your end.   
   
   
---   
   
### A few more examples   
   
   
- `ls ..`   
- `ls ../..`   
- `cat ../../etc/cron.daily/logrotate` - navigating using relative path while you're inside the `Home` dir.   
- Doing the same as above using the absolute path - `cat /etc/cron.daily/logrotate`