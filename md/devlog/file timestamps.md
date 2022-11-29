---
created: 20211017153503812
desc: ''
id: 6jlla2j97qmnmirwouc912w
title: File Timestamps
updated: 1653683931038
---
   
Every file on Linux has three timestamps:   
   
1.  The access timestamp or `atime` is the last time the file was read     
    `ls -lu`   
2.  The modified timestamp or `mtime` is the last time the contents of the file was modified     
    `ls -ls` , `ls -lt`   
3.  The changed timestamp `ctime` is the last time when some metadata related to the file was changed     
    `ls -lc`   
   
<!-- end list -->   
   
   
- To reverse sorts use `-r` or `--reverse`     
  Example: `ls -lu -r` or `ls -lutr` or `ls -lut --reverse`   
   
- Use `ls -l --full-time path` to get entire timestamp.   
   
   
---   
   
   
- The Linux Timestamps has an integer number rather than a date or time.   
- The integer number is the number of seconds since the [Unix Epoch](../devlog/unix%20epoch.md).   
- When a timestamp is needed to be generated, Linux calculates time passed since [Unix Epoch](../devlog/unix%20epoch.md), which makes it easier for humans to understand.   
   
   
---   
   
## The [stat](../archive/STAT.md) command   
   
`stat` is a command-line utility that displays detailed information about given files or file systems.   
   
When invoked without any options, `stat` displays the following file information:   
   
   
- File - The name of the file.   
- Size - The size of the file in bytes.   
- Blocks - The number of allocated blocks the file takes.   
- IO Block - The size in bytes of every block.   
- File type - (ex. regular file, directory, symbolic link.)   
- Device - Device number in hex and decimal.   
- Inode - Inode number.   
- Links - Number of hard links.   
- Access - File permissions in the numeric and symbolic methods.   
- Uid - User ID and name of the owner .   
- Gid - Group ID and name of the owner.   
- Context - The SELinux security context.   
- Access - The last time the file was accessed.   
- Modify - The last time the file’s content was modified.   
- Change - The last time the file’s attribute or content was changed.   
- Birth - File creation time (not supported in Linux).   
   
> —via [Stat Command in Linux](https://linuxize.com/post/stat-command-in-linux/)   
   
   
---   
   
## The [touch](../devlog/touch.md) command   
   
The touch command is a standard program for Unix/Linux operating systems, that is used to create, change and modify timestamps of a file. Before heading up for touch command examples, please check out the following options:   
   
   
- \-a, change the access time only   
- \-c, if the file does not exist, do not create it   
- \-d, update the access and modification times   
- \-m, change the modification time only   
- \-r, use the access and modification times of file   
- \-t, creates a file using a specified time   
   
> —via [8 Practical Examples of Linux "Touch" Command](https://www.tecmint.com/8-pratical-examples-of-linux-touch-command/)   
   
   
- To create a file using `touch` simply: `touch fileName`   
   
   
---   
   
   
- Set timestamps of one file to the timestamps of another file:   
   
`touch fileOne -r fileTwo`   
   
   
- `touch`-ing an existing file will update it's timestamps:   
   
`touch fileName`   
   
   
- It is not possible to modify just the "change" timestamp (the trick is to set the system time to the desired "change" time and `touch` it and adjust the "access" and "modify" time to the initial values)