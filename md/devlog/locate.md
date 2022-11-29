---
created: 20211023070232320
desc: ''
id: tu91wbow964diy55l84cku2
title: locate
updated: 1652815757397
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Not installed by default on Ubuntu as it is on CentOS   
- `mlocate` is the newer implementation of `locate`   
- On latest Linux distros, when you run `locate` it actually runs `mlocate`   
- The `locate` utility works better and faster than the `find` command (locate's counterpart) because instead of searching the file system when a file search is initiated, it would look through a database. This database contains bits and parts of files and their corresponding paths on your system. By default, locate command does not check whether the files found in the database still exist and it never reports files created after the most recent update of the relevant database.   
   
Exit Status: This command will exit with status 0 if any specified match found. If no match founds or a fatal error encountered, then it will exit with status 1.   
   
`sudo updatedb` is used to update the database, this needs to be ran to reflect the latest changes in the file system, its located in `/var/lib/mlocate/mlocate.db`   
   
### Examples   
   
   
- `locate -S` - get statistics about the database   
- `locate passwords` - to list all path names(asbolute) that contains the string "passwords"   
- `locate -b seahorse` -b, –basename, Match only the base name against the specified patterns(it will replace the name with \*name\* implicitly), which is the opposite of –wholename.   
- `locate -b '\name'` - to search for an exact name, it'll stop the implicity replacement of name with `*name*`.   
- `locate -e myfilename123x` - to check if the file really exists in the file system even if it exists on the database   
- `locate -i Rainshadow` - to make locate ignore case   
- `locate -b -r '^shadow\.[0-9]'` - `-r` to use simple [regular expression](../devlog/regular%20expression.md)