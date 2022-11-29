---
created: 20211029081225612
desc: ''
id: vro2wf2ayviwa9mlv92e452
title: netplan
updated: 1665172415074
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`netplan` is used to statically configured a network interface. Typically Laptops and Desktops have their [ip address](../devlog/ip%20address.md) assigned dynamically by a [DHCP](../devlog/dhcp.md) server(in most cases, the [router](../devlog/router.md)), however a server requires a static configuration to avoid single point of failure problem using a [DHCP](../devlog/dhcp.md) server.   
   
`netplan` is default network configuration tool in Ubuntu. It uses [languages.YAML](../devlog/languages.YAML.md) files located in ``/etc/netplan`, it currently supports two renderers or backend services to control network interfaces on Ubuntu based systems, they're [NetworkManager](/not_created.md) and [systemd-networkd](../devlog/systemd-networkd.md).   
   
[NetworkManager](/not_created.md) is commonly used Desktop machines while [systemd-networkd](../devlog/systemd-networkd.md) is used on servers without a [GUI](/not_created.md).