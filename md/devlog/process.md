---
created: 20211028075825684
desc: ''
id: xlsa83es4v1pnpfw5i0k74w
title: process
updated: 1653307887245
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- In Linux, running an instance of a program is called a **process** and it runs in its own memory space. Each time you execute a command, a new process starts.   
- A process is an _active entity_ (whose binary is actively running in the background) as opposed to a program, which is considered to be a _passive entity_.   
- A new process is created only when running an executable file (not when running shell builtin commands, see: [type](../devlog/type.md)).   
- If an executable file doesn't have [suid](../devlog/suid.md) set, then the process has the permission of the user who runs it.   
- `task` and `processes` are synonyms.   
   
### Process properties:   
   
   
- PID (Process ID) - a unique positive integer number   
- User   
- Group   
- Priority/Nice   
   
### Type of Processes:   
   
   
- Parent   
- Child   
- [daemon](../devlog/daemon.md)   
- Zombie(defunct)   
- Orphan   
   
In Linux, all the processes in the OS are created when existing processes invoke the [fork](/not_created.md) system call. There's an execption and that is system boot([init](/not_created.md), [systemd](../devlog/systemd.md) has process ID as `1`).   
   
The process that invokes the [fork](/not_created.md) system call is the parent process and the created process is the child process. A parent may have multiple children but a child can only have one parent.   
   
For example: when you run `who`, bash is the parent(process) that started the child(process) [who](../devlog/who.md)   
   
The OS maintains a table that associates every processes with data necessary for its functioning. When a process is terminated, the OS releases most of the resources and information related to the process.   
   
A terminated process whose data has not been collected is called a Zombie or defunct process. Zombie process are removed quicky and don't use a lot of resources.   
   
Ophan processes are the opposite of Zombie processes, produced when a parent process is terminated before it's child process. By default orphan processes will recieve a hangup call and get terminated.   
   
There is also a possibility of being adopted by another process such as [init](/not_created.md) or [systemd](../devlog/systemd.md) see: [nohop](../devlog/nohop.md)].   
   
   
---   
   
## Threads   
   
Multiple threads can existing within a process and share resources while different processes do not share resources. Threads are basically subprocess that run in the same memory context of a process and make application responsive. Threads may share the same data while executing.