---
created: 20211022174130790
desc: ''
id: j7lpn4vequ39iavpvi1zquu
title: wc
updated: 1652815757472
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
On Linux and Unix-like operating systems, the wc command allows you to count the number of lines, words, characters, and bytes of each given file or standard input and print the result.   
   
The options below allow you to select which counts are printed.   
   
   
- `-l`, –lines - Print the number of lines.   
- `-w,` –words - Print the number of words.   
- `-m`, –chars - Print the number of characters.   
- `-c`, –bytes - Print the number of bytes.   
- `-L`, –max-line-length - Print the length of the longest line.   
   
Example:   
   
`wc /etc/passwd`   
   
Output: `48 83 2825 /etc/passwd` where 48 lines, 83 words and 2825 characters