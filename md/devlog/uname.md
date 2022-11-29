---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: s6jn9xsw9yfzgxcjvcudkd9
title: uname
updated: 1652815757658
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`uname` is a command-line utility that prints basic information about the operating system name and system hardware.   
   
The uname tool is most commonly used to determine the processor architecture, the system hostname and the version of the kernel running on the system.   
   
The options are as follows:   
   
   
- `-s`, (`--kernel-name`) - Prints the kernel name.   
- `-n`, (`--nodename`) - Prints the system’s node name (hostname). This is the name the system uses when communicating over the network. When used with the `-n` option, `uname` produces the same output as the `hostname` command.   
- `-r`, (`--kernel-release`) - Prints the kernel release.   
- `-v`, (`--kernel-version`) - Prints the kernel version.   
- `-m`, (`--machine`) - Prints the name of the machine’s hardware name.   
- `-p`, (`--processor`) - Prints the architecture of the processor.   
- `-i`, (`--hardware-platform`) - Prints the hardware platform.   
- `-o`, (`--operating-system`) - Print the name of the operating system. On Linux systems that is “GNU/Linux”   
- `-a`, (`--all`) - When the `-a` option is used, `uname` behaves the same as if the `-snrvmo` options have been given.   
   
When invoked without any options, `uname` prints the kernel name, as if the `-s` option had been specified   
   
> — via [Uname Command in Linux | Linuxize](https://linuxize.com/post/uname-command-in-linux/)   
   
## Examples   
   
`-a` option to print all available information   
   
```
uname -a
```
