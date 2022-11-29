---
created: '2021-10-28T00:00:00.000Z'
desc: ''
id: laeri4eob3q0wi2i0d71atn
title: top
updated: 1653305465273
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`top` command is used to show the Linux [process](../devlog/process.md)es. It provides a dynamic real-time view of the running system. Usually, this command shows the summary information of the system and the list of processes or threads which are currently managed by the Linux Kernel.   
   
As soon as you will run this command it will open an interactive command mode where the top half portion will contain the statistics of processes and resource usage. And Lower half contains a list of the currently running processes. Pressing `q` will simply exit the command mode.   
   
> —via [top command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/top-command-in-linux-with-examples/)   
   
By default top updates its dislay every 3 seconds and makes a flicker when it updates   
   
   
- Check [Man Pages](../devlog/man%20pages.md) for top: `man top`   
  - `/CPU States`   
  - `/DESCRIPTIONS of Fields`   
- Since `top` interactive, you can press keys such as(press the same key again to turn off)   
  - `h` for help   
  - `z` for highlighting running [process](../devlog/process.md)   
  - `c` will display absolute path of running process   
  - `1` to change display and view statistics for individual CPU   
  - `t` to simple ASCII graph   
  - `m` for memory display options   
  - `d` to change delay value(update or refresh time) and enter new value   
  - `space` to refresh manually   
  - `y` to highlight process and `x` to highlight column   
  - `b` to toggle bold and text highlighting   
  - `<` and '\>' to move between columns   
  - `R` to change order   
  - `e` to change size unit   
  - `P` to sort by processor(CPU)   
  - `M` to sort by memory   
  - `u` to check process by the user, enter username after pressing `u`   
  - `F` to change columns display to enter fields management screen, fields displayed has an `*` asterisk before the name and are highlighted in bold   
    - To select or deslect, press `space`   
    - Press `right` arrow key to select and move with `up` or `down` arrow keys to order the fields. Press `ESC` when you're done.   
  - The changes will be lost when `top` is terminated to make these changes persistent, press `W` to "write" changes.   
   
### Printing changes to a file   
   
`top -d 1 -n 3 -b > top_processes.txt`   
   
   
- \-d for delay   
- \-n for iteration   
- \-b for start/stop in batch mode   
   
To view the differences between each refresh   
   
`grep processName top_processes.txt`   
   
See also: [htop](../devlog/htop.md)