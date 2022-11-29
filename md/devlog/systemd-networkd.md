---
created: 20211029082117660
desc: ''
id: rkxi9ojd57alhi83ezqb41o
title: systemd-networkd
updated: 1665172437103
---
   
Topics::  [networking](../topics/networking.md),[linux](../topics/linux.md)   
   
   
---   
   
[systemd-networkd](../devlog/systemd-networkd.md) is a system [daemon](../devlog/daemon.md) that manages network configurations. It detects and configures network devices as they appear; it can also create virtual network devices. This service can be especially useful to set up complex network configurations for a container managed by systemd-nspawn or for virtual machines. It also works fine on simple connections.   
   
> —via [systemd-networkd - ArchWiki](https://wiki.archlinux.org/title/systemd-networkd)   
   
A network interface can either be managed by [NetworkManager](/not_created.md) or by [systemd-networkd](../devlog/systemd-networkd.md)   
   
Setting up static   
   
   
- Disable [NetworkManager](/not_created.md)   
  - `sudo systemctl stop NetworkManager`   
  - `sudo systemctl disable NetworkManager`   
  - check with `sudo systemctl status NetworkManager` and `sudo systemctl is-enabled NetworkManager`   
- Create a [languages.YAML](../devlog/languages.YAML.md) in `/etc/netplan`, before that you might want to remove the existing [languages.YAML](../devlog/languages.YAML.md) file that was created for NetworkManager to avoid interference.   
- `vim /etc/netplan/01-netconfig.yaml`   
- Each netplan [languages.YAML](../devlog/languages.YAML.md) file starts with the `network` keyword and at least 3 required elements:   
  - `version` of the network configuration format   
  - `renderer`   
  - device type (`ethernets`, `wifis`,`bridges`)   
    - under the devices type you specify one or more network interfaces   
      - `dhcp4` as false(for static configuration)   
      - `addresses` ([ip address](../devlog/ip%20address.md) with [netmask](../devlog/netmask.md))   
      - `gateway4` (default gateway)   
      - `nameservers`   
- Save and exit, to apply `netplan apply`   
- Verify changes `ifconfig` and `route -n`   
- Be careful about [languages.YAML](../devlog/languages.YAML.md)'s indentation and syntax (use an online [languages.YAML](../devlog/languages.YAML.md) validator)   
   
### Examples for [languages.YAML](../devlog/languages.YAML.md) file configurations   
   
Configure an ethernet device with networkd, identified by its name, and enable   
DHCP:   
   
    network:   
      version: 2   
      ethernets:   
        eno1:   
          dhcp4: true   
   
This is an example of a static-configured interface with multiple IPv4 addresses   
and multiple gateways with networkd, with equal route metric levels, and static   
DNS nameservers (Google DNS for this example):   
   
    network:   
      version: 2   
      renderer: networkd   
      ethernets:   
        eno1:   
          addresses:   
   
          - 10.0.0.10/24   
          - 11.0.0.11/24   
          nameservers:   
            addresses:   
   
              - 8.8.8.8   
              - 8.8.4.4   
          routes:   
   
          - to: 0.0.0.0/0   
            via: 10.0.0.1   
            metric: 100   
   
          - to: 0.0.0.0/0   
            via: 11.0.0.1   
            metric: 100   
   
> —via [Netplan Backend-agnostic network configuration in [languages.YAML](../devlog/languages.YAML.md)](https://netplan.io/reference/)