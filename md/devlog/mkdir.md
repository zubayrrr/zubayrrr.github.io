---
created: '2021-10-22T00:00:00.000Z'
desc: ''
id: y4xa97imhwpn9zomq23imf2
title: mkdir
updated: 1653437863959
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`mkdir` command in Linux allows the user to create directories (also referred to as folders in some operating systems ). This command can create multiple directories at once as well as set the permissions for the directories. It is important to note that the user executing this command must have enough permissions to create a directory in the parent directory, or he/she may receive a ‘permission denied’ error.   
   
Syntax:   
   
`mkdir [options...] [directories ...]`   
   
> —via [mkdir command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/mkdir-command-in-linux-with-examples/)   
   
Example:   
   
`mkdir dirName` or `mkdir -v dirName` to make mkdir be verbose about the dir creation   
   
`mkdir dir1 dir/dir2` to create multiple dirs or dirs inside of dirs(dir2 will be created inside dir, dir should already exist in order for dir2 to be created)   
   
`mkdir -p first/second/third` to make mkdir create the parent dirs too along with the child dirs