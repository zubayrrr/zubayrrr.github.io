---
created: 20211023085111772
desc: ''
id: d3d1v1gzr71bjd8nc7jaibf
title: grep
updated: 1653306050503
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`grep` stands for Globally Search For Regular Expression and Print out. It is a command line tool used in UNIX and Linux systems to search a specified pattern in a file or group of files.   
   
Syntax:   
   
   
- grep 'word' filename   
- fgrep 'word-to-search' file.txt   
- grep 'word' file1 file2 file3   
- grep 'string1 string2' filename   
- cat otherfile | grep 'something'   
- command | grep 'something'   
- command option1 | grep 'data'   
- grep –color 'data' fileName   
- grep \[-options\] pattern filename   
- fgrep \[-options\] words file   
   
Examples:   
   
   
- `grep user /etc/ssh/ssh_config` displays all the lines that contains the string "user" inside the file `ssh_config`   
- `grep "command line" /etc/ssh/ssh_config` the string will have to be wrapped in `" "` if it contains multiple words   
- `grep -i "SSH" /etc/ssh/ssh_config` to search case-insensitively   
- `grep -i -n "SSH" /etc/ssh/ssh_config` -n to print the line number of the searched results, you can also group the options such as `-in`   
- `grep -w body /etc/passwd` -w to search for whole word   
- `grep -v kernel /var/log/dmesg` -v to invert the match, will return all the lines that do not contain the string "kernel"   
- `grep -a root /var/log/auth.log` -a to search a binary file (data) as if it were a regular text file.   
- `sudo grep -R 127.0.0.1 /etc` -R to search recursively in all the files inside the `/etc` dir   
- Use `-s` to suppress error messages such as `"Permission denied"`   
- Use `-c` to get just the count for the matched pattern: `grep -c error /var/log/syslog` or     
  `grep error /var/log/syslog | wc -l`   
   
   
---   
   
### Filtering [stdout](../devlog/stdout.md) of other commands using `grep`   
   
   
- `dmesg | grep error`   
- `dmesg | grep -A 3 -B 4 error` will print (-A) 3 lines after and (-B) 4 lines before the string "error"   
- `dmesg | grep -C 3 error` will print (-C) 3 lines before and after the string "error"   
   
<!-- end list -->   
   
   
- `sudo netstat -tupan | grep portNumber`   
   
using [netstat](../devlog/netstat.md), [grep](../devlog/grep.md)   
   
   
- `ls -RF /etc | grep /` to filter the [stdout](../devlog/stdout.md) of [ls](../devlog/ls.md) for dirs or     
  inverse it using -v option `ls -RF /etc | grep -v /` to print all files that are not dirs   
   
- Using [regular expression](../devlog/regular%20expression.md) to exclude empty lines:     
  `ls -Rf /etc | grep -v / | grep -v "^$"` the [regular expression](../devlog/regular%20expression.md) for a space is `^$`, carrot sign for beginning and dollar sign for the end of the line, so exclude anything that has a character in the beginning and the end of a line   
   
- `sudo ls -RF /etc | grep -v / | grep -v "^$" | sort -r | less` sorted by name in reverse alphabetical order, remove `-r` to sort in the alphabetical order   
   
See also: [strings](../devlog/strings.md)