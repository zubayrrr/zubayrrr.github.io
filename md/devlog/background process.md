---
created: '2021-10-28T00:00:00.000Z'
desc: ''
id: w0vd2ayughwv1t1wm0334f3
title: background process
updated: 1653318304086
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Background processes are non interactive and are started by the system services or by the users. While they're running you can start other processes within the same terminal, unlike [foreground process](../devlog/foreground%20process.md)es.   
   
To start a background service append `&` at the end of the command. Simulate this using `sleep 20 &`   
   
Even though it runs in the background, all the errors or outputs to the terminal it was started from.   
   
Since background processes are non interactive, its common to redirect the output or errors to a file.   
   
If you're not interested in a command's output or errors you can redirect it to `/dev/null`. Known as Null device or colloquially known as Blackhole.     
`ping -c 1 google.com > /dev/null 2>&1 &`   
   
   
---   
   
   
- When starting a process in the background, you'll see two numbers in the terminal. Each background process is identified by a Job ID and the [PID](../devlog/pid.md).   
- If you press enter and if the process has completed successfully, you'll get the Job ID and the text `Done` in place of [PID](../devlog/pid.md).   
- You can list the started from the terminal using the [jobs](../devlog/jobs.md) commands.