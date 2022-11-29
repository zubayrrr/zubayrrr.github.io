---
created: 20211015142355030
desc: ''
id: vd667f7oqlww0ermb6y92sn
title: Linux Terminal History
updated: 1652815757651
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- The Linux Terminal command history is saved in `.bash_history` by default.   
- The number of commands saved in the history is controlled by an Environment Variable called $HISTFILESIZE   
- To check $HISTFILESIZE: `echo $HISTFILESIZE`   
- To get the list of commands in history, run `history` in terminal, it'll return a list of commands stored in the memory, determined by the environment variable $HISTSIZE, which is the amount of commands stored in the memory, different from $HISTFILESIZE is the variable that controls the commands saved in `.bash_history`.   
- History file (`.bash_history`) only gets updated when the user logs out.   
- Use `!` followed by the number (`#`) of the command returned from `history` to run the command or `!-#` to run command from the bottom.   
- To search and run a command that was last run in the history: `!commandName`   
- To search and print the command that was last run in the history: `!commandName:p`   
- To navigate through the command history, use Arrow keys or `Ctrl + n` or `Ctrl + p`   
- `Ctrl + r` to so search the history, `Ctrl+ g` to quit and clear the line.   
- To delete something from the history: `history -d #` where \# is the number of command to be deleted from the history.   
- To clear everything from the history: `history -c` and to permanently delete it     
  `history -c; history -w`   
   
   
---   
   
### Run a command without saving it in the history   
   
   
- Add a white space before your command to avoid it from being saved in the history. (this behaviour can differ from distro to distro).   
- $HISTCONTROL is the environment variable that controls if we want to avoid saving a command to the history if it encounters a space before the command.   
- `HISTCONTROL=ignorespace` needs to be set to achieve this funtionality.   
- Existing configuration for $HISTCONTROL can be checked with: `echo $HISTCONTROL`   
- HISTCONTROL can be set to `ignoredups` to avoid duplicate commands from being logged to history or it can be set to `ignoreboth` to utilize both `ignoredups` and `ignorespace`.   
- These variables will only persists for the current session and will be lost if the session is restarted.   
- To append it to the .bashrc file: `echo "HISTCONTROL=ignoreboth" >> .bashrc`   
- set the env variable `HISTTIMEFORMAT="%/d/%m/%y %T"` to get date/time stamp for the `history` command   
- To make these settings persist, they need to be added to the `.bashrc` file.