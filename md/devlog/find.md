---
created: 20211027125521890
desc: ''
id: mx4bqwojj5gg8gvl4mdyvoj
title: find
updated: 1653437393522
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`find` has more options than its counterpart [locate](../devlog/locate.md) command. It can be used to find files and directories and perform subsequent operations on them. It supports searching by file, folder, name, creation date, modification date, owner and permissions.By using the `-exec` option other UNIX commands can be executed on files or folders found. Unlike [locate](../devlog/locate.md) it does real time search on the file system.   
   
### Syntax   
   
`find [where to start searching from] [expression determines what to find] [options] [what to find]`   
   
### Examples   
   
   
- `find . -name todo.txt` - `.` to search in current directory, searches for a `-name` that is `todo.txt`   
- Use `-iname` to make it search case insensitively   
- `find . -name "todo*"` - to look for anything that starts with the string `todo`, its recommended to wrap them inside `" "`   
- `find . -name "*rep*"` - to look for anything that contains the string `"rep"`   
- `find . -name todo.txt -delete` - to find a file and delete it.   
- `find /etc/ -name passwd` - permission denied [stderr](/not_created.md) if the user doesn't have permissions   
- You can run a command after it has found the files, `sudo find /etc/ -name passwd -ls`   
- `find /etc/ -type d` to list all dirs and subdirs recursively   
- `find /etc/ -type d -maxdepth 2` to specify depth of directory traversal   
- `find /etc/ -type d -maxdepth 3 -perm 755 | wc -l` to search by those exact permissions(`-perm 755`) and will also run [[wc] on it.   
- `find /var -type f -size 100k -ls` will look for files(`f`) with size (`100k`) and will run `ls` on the discovered files.   
- `sudo find /var -type f -size +10M -ls` will look for files with size greater than `10M`   
- `sudo find /var -type f -size -10k -ls` will look for files with size less than `10k`   
- Finding files in a range of size: `sudo find /var -type f -size +5M -size -10M`   
- To search by timestamp: `find /var -type f -mtime 0 -ls` files modified in the last 24 hours, `0` since fractional parts are ignore, it really means `0 days ago`   
- `find /var -type f -mtime 1 -ls` files modified `1-2 days ago`   
- `find /var -type f -atime +1 -ls` files last accessed `2 day ago`, `+1` signifies the next number after `1`   
- Use `-amin`, `-mmin`, `-cmin` to search by minutes   
- `find /var -type f -mmin -60` files modified less than 60 mins ago   
- Use `-user`, `-group` to search by owner, group   
- `sudo find /var -type f -user gdm -ls`   
- `sudo find /var -type f -not -group root -ls` to negate an option use `-not`, will find all the files that do not belong to the root group   
   
### Execute a command discovered by the `find` command using `-exec` option   
   
`sudo find /etc -type f -mtime 0 -exec cat {} \;`   
   
   
- will run `cat` on each file found by `find`, `{}` will store the files found `\;` signifies the end of the command.   
   
`sudo find /etc -mtime -7 -type f -exec cp {} /root/backup \;`   
   
   
- Backup all files in `/etc` modified in the last week: `-7` means in the last 7 days, note that the dir `/root/backup` will have to be created first   
- Delete files that were modified 10 mins ago:   
   
`sudo find . -type f -mtime -10 -exec rm {} \; `   
   
   
- Use `-ok` instead of `-exec` to do the same interactively