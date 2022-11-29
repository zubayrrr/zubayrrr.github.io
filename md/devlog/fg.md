---
created: '2021-10-28T00:00:00.000Z'
desc: ''
id: desuvutv1t7setmx8gj70tl
title: fg
updated: 1652815757626
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`fg` command moves a [background job](../devlog/background%20process.md) in the current shell environment into the [foreground](../devlog/foreground%20process.md). Use the job ID parameter to indicate a specific job to be run in the foreground. If this parameter is not supplied, the `fg` command uses the job most recently suspended, placed in the background, or run as a background job.   
   
`fg %JobID`