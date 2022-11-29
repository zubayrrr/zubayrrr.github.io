---
created: 20211022091431344
desc: ''
id: l3leurtotj9lozm4ewqpwrf
title: cp
updated: 1652815757502
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`cp` is a command-line utility for copying files and directories on Unix and Linux systems.   
   
Syntax:   
   
`cp [OPTIONS] SOURCE... DESTINATION`   
   
   
- When the SOURCE and DESTINATION arguments are both files, the cp command copies the first file to the second one. If the file doesn’t exist, the command creates it.   
- When the SOURCE has multiple files or directories as arguments, the DESTINATION argument must be a directory. In this situation, the SOURCE files and directories are moved to the DESTINATION directory.   
- When the SOURCE and DESTINATION arguments are both directories, the cp command copies the first directory into the second one.   
   
To copy files and directories, you must have at least read permissions on the source file and write permission on the destination directory. Otherwise, a permission denied error is shown.   
   
> —via [Cp Command in Linux (Copy Files)](#%20Linuxize%7Chttps%3A%2F%2Flinuxize.com%2Fpost%2Fcp-command-in-linux%2F)   
   
Examples:   
   
   
- `cp /etc/passwd ./users.txt` - since users.txt doesn't exist, `cp` will create it.   
- `cp /etc/groups ./users.txt` - since users.txt already exists, cp will overwrite the contents of `/etc/groups` to users.txt   
- pass the `-v` flag for `cp` to be verbose about the files that are being copied   
- pass the `-i` flag to make `cp` prompt before copying/overwriting.   
- pass the `-r` flag to recursively copy directories and the subdirectories.   
  - `sudo cp -r /etc/ ~/Desktop/`   
- The user that runs `cp` on a file/dir, that user will become the owner of the copied file/dir, file attributes(permissions, ownership, timestamps) are not preserved by default.   
  - pass the `-p` flag to make `cp` preserve the file attributes.