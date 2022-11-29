---
created: 20211012134449204
desc: ''
id: s4ptsgijppmceg9hcdsot7i
title: xargs
updated: 1652947198755
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Picking up here from [Piping](../devlog/piping.md) and [tee](../devlog/tee.md)   
- The xargs come into play for commands that don't accept any [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) to be piped, commands that only accept commad arguments.   
- Example: `echo` command doesn't accept any [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md), it only accepts command args   
- To work around this we first need to convert the [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) into command args and then pipe it.   
- Demonstration:   
   
`date | echo` will not work nor will `date | echo "hello"` work   
   
What will work is:   
   
`date | xargs echo`   
   
you can also pass `echo`'s own command args such as:   
   
`date | xargs echo "hello"` but here it will run its own arg first   
   
To see this in action:   
   
`date | cut -d " " -f 1 | xargs echo`   
   
   
---   
   
   
- Using `cat` to get file names to delete from a file, passing(piping) it as args to `rm` command.   
- Making a file and writing file names to be deleted.   
- `FilesToDelete.txt` contains: date.txt day.txt   
- Now:   
   
`cat FilesToDelete.txt | xargs rm`