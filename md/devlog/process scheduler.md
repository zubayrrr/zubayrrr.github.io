---
created: 20211028101252320
desc: ''
id: wlubl67qke3xleespg7py7z
title: process scheduler
updated: 1652815514872
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
> The process scheduler is responsible for choosing which processes run and for how long. A scheduler is the basic part of a multitasking operating system like Linux.   
>   
> A multitasking operating system gives the illusion that multiple tasks are running at once when in fact there is only a limited set of processors. There are two kinds of multitasking operating systems: preemptive and cooperative.   
>   
> Linux is a preemptive operating system. Preemptive operating systems decide when to stop executing a process, and which new process should begin running. The amount of time a process runs is usually determined before it’s scheduled, this is called the timeslice and it is effectively a slice of the processors time \[1, P. 41\].   
>   
> In cooperative operating systems the scheduler relies on the process to explicitly tell the scheduler that it’s ready to stop (this is often called yielding). Cooperative operating systems have a problem where tasks that don’t yield can bring down the entire operating system. The last mainstream cooperative OSes were Mac OS 9 and Windows 3.1 \[1, P. 42\].   
>   
> The Linux scheduler has gone through several iterations. The latest scheduler—CFS (the Completely Fair Scheduler)—uses the concept of fair scheduling from queue theory \[1, P. 42\].   
>   
> —via [Process Scheduling - CS Notes](https://notes.eddyerburgh.me/operating-systems/linux/process-scheduling)