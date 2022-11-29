---
created: 20211022072818330
desc: ''
id: 1dx3l4bztwh06ip2hg0ly7z
title: less
updated: 1653305633010
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
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