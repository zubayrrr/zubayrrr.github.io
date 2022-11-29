---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: hbcrmipwwrxrhts4y19eqb8
title: systemd
updated: 1652815757400
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
systemd is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as PID 1 and starts the rest of the system.   
   
systemd provides aggressive parallelization capabilities, uses socket and D-Bus activation for starting services, offers on-demand starting of daemons, keeps track of processes using Linux control groups, maintains mount and automount points, and implements an elaborate transactional dependency-based service control logic. systemd supports [SysV](/not_created.md) and [LSB](/not_created.md) init scripts and works as a replacement for [sysvinit](/not_created.md).   
   
Other parts include a logging daemon, utilities to control basic system configuration like the hostname, date, locale, maintain a list of logged-in users and running containers and virtual machines, system accounts, runtime directories and settings, and daemons to manage simple network configuration, network time synchronization, log forwarding, and name resolution.   
   
> — via [systemd](https://systemd.io/)   
   
   
- It’s name comes from System Management Daemon.   
- systemd is the Linux initialisation system during Linux boot and startup process.   
- The Linux boot process has the following phases:   
  - First, the system powers up   
  - Then, the [bootloader](/not_created.md) such as [grub](/not_created.md) loads the kernel.   
  - Then, the kernel loads up initial RAM disk, which loads the system drives and looks for the root file system.  (traditionally known as “userland” components)   
  - Once the kernel is setup - it begins the systemd init system.   
  - systemd starts with PID 1 and takes over and continues to mount the filesystem and starts services.   
   
The first service is `systemd`, in the process list it called as `init` for backwards compatibility.   
   
```
ps -ef | less
```
   
   
   
- systemd starts services in parallel unlike [sysvinit](/not_created.md) which initialises services sequentially.   
   
To display how long boot process took   
   
```
systemd-analyze
```
   
   
To print all running units by the time it took for them to initialise   
   
```
systemd-analyze blame
```
   
   
## service/unit   
   
In `systemd`, the target of most actions are “units”, which are resources that `systemd` knows how to manage. Units are categorized by the type of resource they represent and they are defined with files known as unit files. The type of each unit can be inferred from the suffix on the end of the file.   
   
Although it is technically correct to classify a unit as a service, in systemd, units tend to be more abstract and often comprised of resource pools, filesystem mounts, network protocols, devices, and native Linux services.   
   
Units are defined in a file known as a Unit file. Systemd can manage unit files from any location, but their main location is `/etc/systemd/system` directory. Unit files in this directory are mainly user-provided. Compared to other locations, the systemd manager will assign higher precedence to unit files within the above directory.   
   
```
sudo systemctl list-units

# or

sudo systemctl list-units --all

# to show all installed unit files

sudo systemctl list-unit-files
```
   
   
The following are the unit files found in systemd.   
   
   
- **.service** – Service unit files define how systemd manages a service. They typically end in .service extension. Service unit files describe how to start, stop, reload and restart a service and the dependencies required to manage the service.   
- **.target** – Target units provide synchronization points to other services during startup.   
- **.slice** – slice unit files encode information about systemd slice units. Slice units are part of the Linux control group tree that allows resource allocation and restriction to processes associated with a slice. You can learn more about systemd resource control [here](https://www.freedesktop.org/software/systemd/man/systemd.resource-control.html).   
- **.socket** – A socket unit file encodes information about network socket, IPC, or a file system FIFO buffer controlled and managed for systemd, which systemd uses for socket-based activation.   
- **.device** – Device unit configurations define a device unit as exposed in the sysfs/udev device tree.   
- **.timer** – Timer units define a timer managed and controlled by systemd for scheduled activation.   
- **.snapshot** – Snapshot unit files allow rollback of the current state of the system after making changes. We create them using the systemd snapshot command.   
- **.swap** – Swap units encode information about swap space, such as the device name or path of the swap space.   
- **.mount** – mount unit files encode information about mount points in the system managed by systemd.   
- **.automount** – these are unit files that define mount points that are automatically mounted.   
   
## systemctl   
   
`systemctl` is a Linux command-line utility used to control and manage systemd and services. You can think of Systemctl as a control interface for Systemd init service, allowing you to communicate with systemd and perform operations.   
   
Systemctl is a successor of Init.d system; it contains libraries, daemons, and utilities you can use to manage services in the Linux system.   
   
To start a `systemd` service, executing instructions in the service’s unit file, use the `start` command. If you are running as a non-root user, you will have to use `sudo` since this will affect the state of the operating system:   
   
```
sudo systemctl start application.service

# or you can skip .service

sudo systemctl start application
```
   
   
To stop/restart   
   
```
sudo systemctl stop application
sudo systemctl restart application
```
   
   
restart vs reload   
   
`restart` will terminate the service in question and restart it; `reload` will only reload the configuration file of the service. Not all services might support `reload` in which case you can use `reload-or-restart`   
   
To check status   
   
```
sudo systemctl status application
```
   
   
To enable or disable   
   
`enable` will enable a service to start automatically at boot time vice versa for `disable`   
check with `is-enabled` (these settings only take place at boot time and won’t effect current session)   
   
```
sudo systemctl enable application
```
   
   
To see a unit’s dependency tree   
   
```
systemctl list-dependencies sshd.service
```
   
   
Masking   
   
`systemd` also has the ability to mark a unit as *completely* unstartable, automatically or manually, by linking it to `/dev/null`. This is called masking the unit, and is possible with the `mask` command:   
   
This will prevent the Nginx service from being started, automatically or manually, for as long as it is masked.   
   
```
sudo systemctl mask nginx.service

# to unmask

sudo systemctl unmask nginx.service
```
   
   
## References   
   
   
- [How To Use Systemctl to Manage Systemd Services and Units | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)   
- [How to Use Systemctl Utility in Linux](https://linuxhint.com/systemctl-utility-linux/)   
- [Systemd Units Explained with Types and States](https://www.computernetworkingnotes.com/linux-tutorials/systemd-units-explained-with-types-and-states.html)