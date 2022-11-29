---
created: '2021-10-22T00:00:00.000Z'
desc: ''
id: qac731114j07bzuspuc1duf
title: Viewing Files
updated: 1653305633004
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- The entire configuration of a Linux system is stored on a text tle.   
- Things such as FTP, email server, network configuration, security policy, users and their passwords, groups are also stored on a text file.   
- There are many ways to read a text file on Linux.   
- You can use graphical text editors(Gedit, Kate etc) to view text files as well has CLI editors.   
   
   
---   
   
## Commands available to view text files and to keep track of files in real time   
   
### [cat](../devlog/cat.md) command   
   
   
- `cat` command allows us to:   
  - Create single or multiple files   
  - View contents of file   
  - Concatenate files   
  - Redirect output in terminal or files.   
- Syntax:   
  - `cat path-to-file`   
- Notes:   
  - Most useful when viewing small files because larger files get when viewed get wrapped due to scrolling limitations.   
  - Usually no options are passed when using `cat` command but   
    - `cat -n path-to-file` will list the line numbers too.   
  - To concatenate: `cat file1 file2 > new_file`   
    - `new_file` would contain the contents of both `file1` and `file2`   
   
### If the output of the text file exceeds the terminal window, we can use `more` or `less` command   
   
### [less](../devlog/less.md) command   
   
   
- `less` is a command line utility that displays the contents of a file or a command output, one page at a time. It is similar to [more](/not_created.md), but has more advanced features and allows you to navigate both forward and backward through the file.   
- When starting less doesn’t read the entire file it reads the contents of a file one page(one screen) at a time which results in much faster load times compared to text editors like [[vim] or [nano](/not_created.md) .   
- The less command is mostly used for opening large files .   
- Syntax:   
  - `less path-to-file`   
- Notes:   
  - [Man Pages](../devlog/man%20pages.md) launch the `less` command by default   
  - `Ctrl + F` or `space` to move forwards one window   
  - `Ctrl + B` to move backwards one window   
  - `g` to go to the very beginning of the file   
  - `G` to go to the very end of the file   
  - To search a string from the very top of the file, press `/` and type the string   
    - Use `n` or `N` to navigate between the search results   
  - To search from the bottom of the file, press `?` and type the string   
   
### [tail](../devlog/tail.md) command   
   
It is the complementary of [head](../devlog/head.md) command.The tail command, as the name implies, print the last N number of data of the given input. By default it prints the last 10 lines of the specified files. If more than one file name is provided then data from each file is precedes by its file name.   
   
> —via [Tail command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/tail-command-linux-examples/)   
   
   
- Syntax:   
  - `tail path-to-file`   
  - `tail -n number path-to-file` to view custom number of lines   
  - `tail -n +20 path-to-file` to views lines from the line \# 20   
- `tail` is most commonly used to watch log files as they're updated   
  - `tail -f path-to-file` to watch the file in real time as it gets updated   
- Example:   
  - `tail -n 15 -f /var/log/auth.log`   
   
### [head](../devlog/head.md) command   
   
It is the complementary of [tail](../devlog/tail.md) command. The head command, as the name implies, print the top N number of data of the given input. By default, it prints the first 10 lines of the specified files. If more than one file name is provided then data from each file is preceded by its file name.   
   
> —via [Head command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/head-command-linux-examples/)   
   
   
- Example:   
  - `head /etc/passwd`   
  - `head -n -7 /etc/group` to view first 7 groups   
   
### [watch](../devlog/watch.md) command   
   
   
- `watch` is used to run any arbitrary command at regular intervals and displays the output of the command on the terminal window.   
- It is useful when you have to execute a command repeatedly and watch the command output change over time. For example, you can use the watch command to monitor the system uptime or disk usage.   
- The watch utility is a part of the [procps](/not_created.md) (or [procps-ng](/not_created.md)) package which is pre-installed on nearly all Linux distributions.   
- You can use `-d` flag to view difference between two successive updates, `-n` option to change the update interval time.   
- Examples:   
  - `watch -n 3 -d ls -l`   
  - `watch date`   
  - `watch ls`   
  - `watch -n 1 -d ifconfig` to keep track of network traffic