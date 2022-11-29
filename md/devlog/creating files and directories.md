---
created: 20211022083351480
desc: ''
id: e26xfb87b3du1j0omk99ko2
title: Creating Files and Directories
updated: 1653437420501
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- [touch](../devlog/touch.md) can be used to create files if they don't already exist.   
- Simply: `touch fileName` or `touch "file name"` to create a file, Linux doesn't recommend file names that contains spaces use an underscore instead.   
- The user should also have the permissions to create files in that directory.   
   
## Creating files using [mkdir](../devlog/mkdir.md)   
   
`mkdir` command in Linux allows the user to create directories (also referred to as folders in some operating systems ). This command can create multiple directories at once as well as set the permissions for the directories. It is important to note that the user executing this command must have enough permissions to create a directory in the parent directory, or he/she may receive a ‘permission denied’ error.   
   
Syntax:   
   
`mkdir [options...] [directories ...]`   
   
> —via [mkdir command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/mkdir-command-in-linux-with-examples/)   
   
Example:   
   
`mkdir dirName` or `mkdir -v dirName` to make mkdir be verbose about the dir creation   
   
`mkdir dir1 dir/dir2` to create multiple dirs or dirs inside of dirs(dir2 will be created inside dir, dir should already exist in order for dir2 to be created)   
   
`mkdir -p first/second/third` to make mkdir create the parent dirs too along with the child dirs