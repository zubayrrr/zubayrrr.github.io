---
created: 20211003114315384
desc: ''
id: u6ip344yfmr12tt108cif3y
title: PC Configuration Scenarios
updated: 1652622338921
---
   
### Gaming System   
   
   
- First thing to consider when making a gaming PC is the PSU   
- Video cards draws a lot of watts of power   
- Ensure motherboard has enough slots for extensions such as video cards, RAM, etc   
- CPU Speed and number of cores   
- RAM for OS and the games   
- GPU on the high-end video card   
- High-end sound card   
- Gaming controller   
- [SSD](../devlog/ssd.md)] storage   
   
### Graphic Design System   
   
   
- CPU speed and number of cores   
- RAM for OS, apps, cached large files   
- High-end video card with GPU   
- [SSD](../devlog/ssd.md)] storage   
- Touchpad   
- Drawing pad such as a Bamboo device   
   
### A/V Editing System   
   
   
- CPU speed and number of core   
- RAM for OS, apps, cached large files   
- [SSD](../devlog/ssd.md)] storage   
- Dual monitors   
- High-end video card GPU   
- High-end sound card   
- Camera   
   
### Virtualization Host   
   
   
- Hypervisor runs virtual machines for running multiple OSs within their own containerized environments simultaneously.   
- Type 1: Bare metal: Is installed directly on the physical hardware; it is _the_ OS itself. Examples include: Microsoft Hyper-V(doesn't require Windows Server to be installed first or VMWare EXSi).   
- Type 2: Runs on top of existing OS. Examples include VMware Workstation running on top of Windows laptop   
   
Type 1 gives best performance in terms of Hypervisors.   
   
   
---   
   
   
- CPU speed and number of cores   
- RAM for Hypervisor + VM guests   
- Dynamic memory allocation for smart utilization of RAM   
- Failover clustering of VMs   
   
#### Fast disk subsystem   
   
   
- Reduce VM guest disk contention   
- Local or network   
   
#### Multiple NICs   
   
   
---   
   
### Thin/Thick Clients for Office use   
   
#### Thin Client   
   
   
- Requires little computing power   
- Does not have local mass storage   
- The OS is stored on the device's firmware itself   
   
#### Thick Client   
   
   
- Local mass storage   
- Requires more compute power   
   
### POS Systems(Point Of Sales)   
   
   
- Card readers   
- Signature pad   
- Need to be patched regularly when updates are available.   
- User accounts to authorize/authenticate cloud accounts/clients   
- SSO - Single Sign On   
- Long passwords, multifactor authentication, touchscreen driver   
- Cloud Sync