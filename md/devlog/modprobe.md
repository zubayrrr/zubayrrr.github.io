---
created: 1657956155343
desc: ''
id: zc07c3csgkbi5tqz365qscn
title: Modprobe
updated: 1657956345453
---
   
Related::  [linux](../topics/linux.md)   
   
   
---   
   
The `modprobe` command allows you to add and remove Linux kernel modules.   
   
## Adding Kernel Modules   
   
The Kernel modules are stored in the `/lib/modules/<kernel_version>` directory. You find the [version of the running kernel](https://linuxize.com/post/how-to-check-the-kernel-version-in-linux/) , use the `uname -r` command.   
   
Only users with administrative privileged can manage Kernel modules.   
   
To load a module, invoke the `modprobe` command followed by the module name:   
   
```
modprobe module_name
```
   
   
The `modprobe` command will load the given module and any additional module dependencies. Only one module can be specified at the command line.   
   
Use the `lsmod` command to confirm that the module is loaded:   
   
```
lsmod | grep module_name
```
   
   
To load a module with additional parameters, use the `parameter=value` syntax:   
   
```
modprobe module_name parameter=value
```
   
   
The command accepts multiple `parameter=value` pairs separated by space.   
   
Generally, you would need to load the module during the system boot. You can do that by that by specifying the module and its parameters in a file inside the `/etc/modules-load.d` directory. Files must end with `.conf` and can have any name:   
   
`/etc/modules-load.d/module_name.conf`   
   
```ini
option module_name parameter=value
```
   
   
Copy   
   
The settings specified in these files are read by `udev`, which loads the modules at system startup using `modprobe`.   
   
## Removing Kernel Modules [#](https://linuxize.com/post/modprobe-command-in-linux//#removing-kernel-modules)   
   
To remove a module, invoke the `modprobe` command with the `-r` option followed by the module name:   
   
```
modprobe -r module_name
```
   
   
`modprobe` will also remove the unused module dependencies.   
   
When invoked with `-r`, the command accepts multiple modules as arguments:   
   
```
modprobe -r module_name1 module_name2
```
   
   
You can also use the `rmmod` command to unload a module from the Linux Kernel.   
   
If you want to prevent a Kernel module from loading at boot time, create a `.conf` file with any name inside the `/etc/modprobe.d`. The syntax is:   
   
`/etc/modprobe.d/blacklist.conf`   
   
```ini
blacklist module_name
```
   
   
If you want to blacklist additional modules, specify the modules on a new line, or create a new `.conf` file.   
   
Via - [Modprobe Command in Linux | Linuxize](https://linuxize.com/post/modprobe-command-in-linux/)