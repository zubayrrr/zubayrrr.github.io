---
created: 20211022093125710
desc: ''
id: 7f96pdsdnu2h6rccq6rr4l9
title: mv
updated: 1652815514816
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The mv command (short from move) is used to rename and move and files and directories from one location to another.   
   
Syntax:   
   
`mv [OPTIONS] SOURCE DESTINATION`   
   
The SOURCE can be one, or more files or directories, and DESTINATION can be a single file or directory.   
   
   
- When multiple files or directories are given as a SOURCE, the DESTINATION must be a directory. In this case, the SOURCE files are moved to the target directory.   
- If you specify a single file as SOURCE, and the DESTINATION target is an existing directory, then the file is moved to the specified directory.   
- If you specify a single file as SOURCE, and a single file as DESTINATION target then you’re renaming the file .   
- When the SOURCE is a directory and DESTINATION doesn’t exist, SOURCE will be renamed to DESTINATION. Otherwise if DESTINATION exist, it be moved inside the DESTINATION directory.   
   
To move a file or directory, you need to have write permissions on both SOURCE and DESTINATION. Otherwise, you will receive a permission denied error.   
   
Example:   
   
   
- `mv file1 /tmp`, `file1` from the current working dir will be moved to `/tmp`   
- `mv file1 file2`, `file1` will be renamed to `file2`   
- `mv -i file1 /tmp` to make `mv` prompt before overwriting if `file1` already exists in `/tmp` where `-i` stands for interactive   
- The `-n` option tells mv never to overwrite any existing file:   
  - `mv -n file1 /tmp`   
- The `-u` option stands for `--update` will only overwrite a file if the destination file is older(only newer files will be moved)   
- Renaming and moving at the same time:   
  - `mv dir10/c.txt dir10/dir2/cc.txt`