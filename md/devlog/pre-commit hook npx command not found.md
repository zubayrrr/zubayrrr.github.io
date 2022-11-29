---
created: 1652622343852
desc: ''
id: 230zh29jy1ptmkvzjurejzx
title: Pre Commit Hook Npx Command Not Found
updated: 1652622343852
---
   
I've got the solution from here. Hope you can find it as well!   
   
   
-   [https://typicode.github.io/husky/#/?id=command-not-found](https://typicode.github.io/husky/#/?id=command-not-found)   
-   [https://github.com/typicode/husky/issues/912](https://github.com/typicode/husky/issues/912)   
   
Here it is, for clarity:   
   
   
-   add a file `~/.huskyrc` if you don't have one already   
-   make sure it includes the following:   
   
```
# ~/.huskyrc
# This loads nvm.sh and sets the correct PATH before running hook
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```
