---
created: 20211022071732050
desc: ''
id: r3ndxve356r9xbujnl3ysp2
title: cat
updated: 1652815514848
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
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