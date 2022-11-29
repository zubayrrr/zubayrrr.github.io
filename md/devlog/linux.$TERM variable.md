---
created: 1662682630039
desc: ''
id: c2m4vz8hplf0986wmhj32m7
title: $TERM variable
updated: 1662682785750
---
   
Topics::  [linux](../topics/linux.md)   
Related::  [environment variable](../devlog/environment%20variable.md)   
   
   
---   
   
The $TERM is an environmental variable in Linux and Unix shell environments. This variable defines the terminal type. In other words, it sets the terminal type for which output is to be prepared.   
   
We can use the `echo` command or `printf` command as follows to see the current value of the `$TERM` variable:   
   
```bash
echo "$TERM"
printf "The current terminal is %s\n" "$TERM"
export TERM=xterm-256color
```
   
   
— via [$TERM variable - Linux Bash Shell Scripting Tutorial Wiki](https://bash.cyberciti.biz/guide/%24TERM_variable)