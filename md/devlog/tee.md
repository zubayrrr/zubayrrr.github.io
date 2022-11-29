---
created: 20211012132455880
desc: ''
id: mekmie4q7zrovcr0dmvzuqh
title: tee
updated: 1652947230097
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
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