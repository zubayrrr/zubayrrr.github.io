---
created: 20211012141734164
desc: ''
id: qj2j8vs4rumzknty271dz04
title: Aliases
updated: 1652948916771
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Aliases for commands   
- Nicknames for your pipelines   
- To get started you need a file in your user's `Home` dir named `.bash_aliases`   
- Write the command inside the `.bash_aliases` file after writing `alias aliasName='command1 -opt args | command2 -opt args ...'` or alias for command that don't accept [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md) can be acheived by `alias aliasName='xargs command -opt args...'`   
- Example:   
   
`alias getdates='date | tee /home/user/date.txt | cut -d " " -f 1 | tee /home/user/day.txt | xargs echo hello'`   
   
   
- You can also build piplines using multiple aliases, the first command in an alias should accept [Redirecting stdin & stderr](../devlog/redirecting%20stdin%20%26%20stderr.md)   
- Terminal will have to be rebooted after creating an alias.   
   
## List all aliases   
   
```bash
alias
```
   
   
## Escape an alias / run the original command   
   
Use `\` to escape an alias   
   
```bash
\ls
```
   
   
## Create an alias   
   
This will create an alias for the existing session. To make aliases persist in all of your user session, create them inside in your `~/.zshrc`, `~/.bashrc`, `~/.bash_profile` (and reload the shell or run `source ~/.zshrc`).   
   
```bash
alias ls="ls -ltr"
```
   
   
## Remove an alias   
   
```bash
unalias ls
```
