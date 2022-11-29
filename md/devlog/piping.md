---
created: 20211012130708336
desc: ''
id: duu1hv74c23zfwgnsoq22i9
title: Piping
updated: 1653305638879
---
   
   
- The Pipe Symbol `|`   
- Redirecting [stdout](../devlog/stdout.md) of a command as [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) of another command is known as Piping.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.xa8e0nfb4zr.png)   
   
   
- Example: passing stdout from date using `|` symbol as the stdin for the [cut](../devlog/cut.md) command and then outputting ([redirecting](../devlog/stdout.md)) it in a file `date.md` using `>` symbol.   
   
`date | cut --delimiter=" " --fields=1 > date.md`   
   
   
- We can also use the short forms   
   
`date | cut -d " " -f 1 > date.md`   
   
   
- We can also pass the [stdout](../devlog/stdout.md) as [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) yet again using `|` symbol like   
   
`date | cut -d " " -f 1 | command -opt args ...`   
   
so on and so forth   
   
Examples:   
   
   
- `ls -lSh /etc/ | head`   
- `ls -lSh /etc/ | head -n 20 | tail -n 1`   
   
<!-- end list -->   
   
   
- `cat -n /var/log/auth.log | grep -a "authentication failure"`   
- `cat -n /var/log/auth.log | grep -a "authentication failure" | wc -1` using [cat](../devlog/cat.md), [grep](../devlog/grep.md) and [[wc]   
   
   
---   
   
### The [tee](../devlog/tee.md) command   
   
   
- Picking up here from [Piping](../devlog/piping.md)   
- By default redirection of [stdout](../devlog/stdout.md) breaks pipelines, unless the `tee` command is used.   
- We use `tee` command to continue using [stdout](../devlog/stdout.md) after redirecting it.   
- The `tee` command helps us with data flow in two directions:   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.mgl2zixejh.png)   
   
   
- Example:   
  - `date | tee date.md | cut -d " " -f 1 > day.md`   
    - Not only are we saving the full date inside `date.md` using the `tee` command but we are also saving the day inside `day.md`.   
    - `date | tee date.md | cut -d " " -f 1 | tee day.md | command -opt args ...` to keep using [stdout](../devlog/stdout.md)   
   
### Another Example using [ifconfig](../devlog/ifconfig.md) and [grep](../devlog/grep.md)   
   
   
- `ifconfig | grep ether` just prints [stdout](../devlog/stdout.md)   
- `ifconfig | grep ether > mac.txt` only redirects [stdout](../devlog/stdout.md) to `mac.txt` without printing it out to the screen   
   
Combining these two using the `tee` command   
   
   
- `ifconfig | grep ether | tee mac.txt` now it would both create the file `mac.txt` and also print out the [stdout](../devlog/stdout.md)   
   
### Append Option   
   
   
- Passing the `-a` option to the `tee` command would instruct it to append the [stdout](../devlog/stdout.md) when redirecting it to a file instead of overwriting it.   
- Example:   
  - `who | tee -a who.txt`   
  - `uname -r | tee -a who.txt kernel.txt` would append the kernel version to both `who.txt` as well as `kernel.txt`   
   
   
---   
   
### The [xargs](../devlog/xargs.md)\ command   
   
   
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