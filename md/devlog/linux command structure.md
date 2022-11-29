---
created: 20211015130033550
desc: ''
id: hyaqtegs5lv6k2c2bxvfp92
title: Linux Command Structure
updated: 1653306010719
---
   
   
- All Linux commands have a structure to them: `commandName -opt args ...`   
- For example: `ping -c 1 8.8.8.8`   
- Where `ping` is the command, `-c` is the option of the command, options are always preceded with `-` hyphen and `8.8.8.8` is the argument.   
- Command name, options, arguments are usually separated with a white space.   
- The options and arguments can flip their positions but the convention is to write the options before the arguments and after the command name.   
- Passing arguments can be mandatory for _some_ commands. (such as `ping`)   
- Options can be combined, they can also be written in both short and long forms in conjunction.   
- Example: `df -hi -all`, where `-hi` are the short form and `--all` is the long form of `-a` which are options for [df](../devlog/df.md) command.