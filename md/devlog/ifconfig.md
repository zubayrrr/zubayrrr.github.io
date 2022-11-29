---
created: 20211029071146350
desc: ''
id: osajilt9rsnrz5ng14pmy8x
title: ifconfig
updated: 1653437745112
---
   
Topics::  [linux](../topics/linux.md),[networking](../topics/networking.md)   
   
   
---   
   
`ifconfig` (interface configuration) command is used to configure the kernel-resident network interfaces. It is used at the boot time to set up the interfaces as necessary. After that, it is usually used when needed during debugging or when you need system tuning. Also, this command is used to assign the IP address and netmask to an interface or to enable or disable a given interface.   
   
   
- `ifconfig` cannot display [default gateway](/not_created.md) nor the [dns](../devlog/dns.md) but the [route](../devlog/route.md) command from `net-tools` can do it.   
- Newer alternative to `ifconfig` is [ip](../devlog/ip.md)   
   
### Examples   
   
   
- To display a list of network interfaces and the associated [ip address](../devlog/ip%20address.md):   
  - `ifconfig -a` -a flag makes it display info about all interfaces but enabled and disabled. If you omit `-a` flag it'll display info only about enabled interfaces.   
- Also displays how many packets and bytes were recieved and transmitted on each inteface.   
- To get info about specific network inteface:   
  - `ifconfig enp0s3`   
- To turn an interface off/on:   
  - `ifconfig enp0s3 down`   
  - The interface will be down(disabled) and will not be previewed when ran `ifconfig`, use `ifconfig -a` to display it.   
- To assign a new [ip address](../devlog/ip%20address.md);   
  - `ifconfig enp0s3 192.168.0.111/24 up` `/24` is the [netmask](../devlog/netmask.md)   
- To change the [MAC](../devlog/mac.md) Address:   
  - Disable the interface: `ifconfig enp0s3 down`   
  - `ifconfig enp0s3 hw ether 08:00:27:51:05:09`   
  - Bring the interface back up: `ifconfig enp0s3 up`