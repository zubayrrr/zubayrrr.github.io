---
created: '2021-10-17T00:00:00.000Z'
desc: ''
id: a25t7tco2lrqbkbppyp43ow
title: touch
updated: 1652815757209
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The touch command is a standard program for Unix/Linux operating systems, that is used to create, change and modify timestamps of a file. Before heading up for touch command examples, please check out the following options:   
   
   
- -a, change the access time only   
- -c, if the file does not exist, do not create it   
- -d, update the access and modification times   
- -m, change the modification time only   
- -r, use the access and modification times of file   
- -t, creates a file using a specified time   
   
> —via [8 Practical Examples of Linux "Touch" Command](https://www.tecmint.com/8-pratical-examples-of-linux-touch-command/)   
   
   
- To create a file using `touch` simply: `touch fileName`   
   
   
---   
   
   
- Set timestamps of one file to the timestamps of another file:   
   
`touch fileOne -r fileTwo`   
   
   
- `touch`-ing an existing file will update it's timestamps:   
   
`touch fileName`   
   
   
- It is not possible to modify just the "change" timestamp (the trick is to set the system time to the desired "change" time and `touch` it and adjust the "access" and "modify" time to the initial values)