---
created: 1653307862379
desc: ''
id: 18r0edfsklpzmjv2acfoous
title: sshd
updated: 1653307862379
---
   
Topics::  [networking](../topics/networking.md), [linux](../topics/linux.md)   
   
   
---   
   
> sshd is the OpenSSH server process. It listens to incoming connections using the SSH protocol and acts as the server for the protocol. It handles user authentication, encryption, terminal connections, file transfers, and tunneling. — via [Sshd is the Linux OpenSSH server process. How to install, setup, and diagnose.](https://www.ssh.com/academy/ssh/sshd)   
   
   
- `d` as in [daemon](../devlog/daemon.md)   
   
### Securing the OpenSSH Server (sshd)   
   
   
- Default installation of SSH isn’t secure, it needs some hardening.   
- The SSH server has a configuration file, usually `/etc/sshd/sshd_config`. The configuration file specifies encryption options, authentication options, file locations, logging, and various other parameters.   
- Edit `sshd_config` for making any changes to the server and restart the server.   
- Backup the file before making changes to it.   
- Change default port from `Port 22` to a random port number   
  - This is security by obscurity   
  - Not the best security practice but highly recommended   
  - Hackers could scan for specific Port 22 or they could also scan all the ports but in case of [ssh](../devlog/ssh.md) most of the time the attacks are not targeted but automated.   
  - Don’t forget to make the changes to the firewall rules to allow the newly defined port.   
- Disable direct root login through [ssh](../devlog/ssh.md)   
  - `#PermitRootLogin prohibit-password` is default; which means you can login as root using a different method such as [Public Key Authentication](/not_created.md) but it is recommended to change it to `#PermitRootLogin no`   
- Disable password authentication   
- List the users that have ssh access under `AllowUsers`   
- Filter ssh access at the firewall level, limit the access of ssh from a predefined list of source [ip address](../devlog/ip%20address.md)ess   
- An example rule is defined below   
- `iptables -A INPUT -p tcp --dport 2278 -s 2.2.4.5 -j ACCEPT`   
- Drop access for all the other IP Addresses   
- `iptables -A INPUT -p tcp --dport 2278 -j DROP`   
- Use SSH protocol version 2   
- Set idle timeout interval   
  - `ClientAlive`   
- `MaxAuthTries` max number of authentication attempts   
- `MaxStartups` max number of concurrent unauthenticated connections to the SSH daemon   
- `LoginGraceTime` the server disconnects after this time if the user has not successfully logged in.   
- Always use latest version of [ssh](../devlog/ssh.md)