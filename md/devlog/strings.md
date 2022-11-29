---
created: 20211023093609600
desc: ''
id: dv7wz70z5zyf5z9yqe0hnd4
title: strings
updated: 1652818345929
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Binary files—such as program files—may contain strings of human-readable text.   
- The Linux strings command pulls those bits of text—called “strings”—out for you.   
- If you use [cat](../devlog/cat.md) or [less](../devlog/less.md) you are likely to end up with a hung terminal window. Programs that are designed to work with text files don’t cope well if non-printable characters are fed through them.   
- Most of the bytes within a binary file are not human readable and cannot be printed to the terminal window in a way that makes any sense. There are no characters or standard symbols to represent binary values that do not correspond to alphanumeric characters, punctuation, or whitespace. Collectively, these are known as “printable” characters. The rest are “non-printable” characters.   
   
> —via [How to Use the strings Command on Linux](https://www.howtogeek.com/427805/how-to-use-the-strings-command-on-linux/)   
   
   
- There could also be `help` info embedded inside the binary file of the program, copyright and other miscellaneous info about the program.   
   
Examples:   
   
   
- `strings /usr/bin/ls | less` will print all the [ASCII](/not_created.md) characters embedded the binary file of [ls](../devlog/ls.md)   
- `sudo strings -a /dev/sda5` to prints out all the [ASCII](/not_created.md) chracters on the device file   
- To search in the machine's physical memory:   
  - `sudo strings /dev/mem | less` will throw all the printable characters in the physical memory