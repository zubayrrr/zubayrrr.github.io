---
created: 1660751643067
desc: ''
id: 5v2tgqm25md5x86kft6utgy
title: Glob
updated: 1660751777317
---
   
Topics::  [linux](../topics/linux.md), [computer science](../topics/computer%20science.md)   
   
   
---   
   
In computer programming, glob patterns specify sets of filenames with wildcard characters. For example, the Unix Bash shell command `mv *.txt textfiles/` moves (`mv`) all files with names ending in `.txt` from the current directory to the directory textfiles. Here, `*` is a wildcard standing for "any string of characters except `/"` and `*.txt` is a glob pattern. The other common wildcard is the question mark (`?`), which stands for one character. For example, `mv ?.txt shorttextfiles/` will move all files named with a single character followed by `.txt` from the current directory to directory `shorttextfiles`, while `??.txt` would match all files whose name consists of 2 characters followed by `.txt`.