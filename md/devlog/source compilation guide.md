---
created: '2022-05-12T00:00:00.000Z'
desc: ''
id: 0nscih3s2fmjawydezj2ppp
title: Source Compilation Guide
updated: 1654011821358
---
   
Topics::  [C Language](../devlog/C%20Language.md), [linux](../topics/linux.md)   
   
   
---   
   
Compiling C Programs from source code. Servers need to be compiled and are generally written in C and C++ Programming languages.   
   
## Source Compilation Guide   
   
   
- Install the prerequisites such as: gcc, g++, make   
- Download the source files of the program you want to compile from its official website.   
- Check the integrity of the tarball (hash or digital signature)   
- Extract the archive and move into the resulting directory   
- Run `./configure --help` and set the required compilation options   
- Run `make`   
- Run `make install`   
   
### Advantages   
   
   
- You can compile applications with certain options that may be missing or disabled in the standard distribution package.   
- Access to the latest version of the application   
- It is possible to have multiple versions of the same program installed.   
   
### Disadvantages   
   
   
- The package manager will be completely unaware of the changes you’ve made. It won’t be possible to update or remove the application using the package manager.   
- If you’re not careful when compiling to install the program to a separate location you can break your system.   
- It can be cumbersome.