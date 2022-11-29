---
caption: Secure Shell
created: 1653574050421
desc: ''
id: o922t6d9q6wur3yve290hir
title: SSH
updated: 1653574050421
---
   
Topics::  [linux](../topics/linux.md),[networking](../topics/networking.md)   
   
   
---   
   
   
- Secure Shell or Secure Socket Shell, operates on [Port 22](/not_created.md)   
- Cryptographic network protocol for operating network services securely, even over an unsecured network.   
- Best known for remote login to computer systems by users.   
   
   
---   
   
   
- The SSH protocol is used for:   
  - Secure Remote Management of Servers, Routers and other Networking Devies.   
  - Network File Copy: [rsync](../devlog/rsync.md), [sftp](../devlog/sftp.md), [sc](/not_created.md) If you suspect a firewall issue then use [ufw](../devlog/ufw.md), [winscp](/not_created.md)   
  - Tunneling, SSH Port Forwarding   
- [SSHD](../devlog/sshd.md) is the SSH server [daemon](../devlog/daemon.md), `ssh` or `putty` are the clients   
   
   
- To check status of ssh   
  - `sudo systemctl status ssh`   
- Service Stop, Restart, Start: `sudo systemctl [start|restart|stop] ssh`   
- Enable, Disable auto booting: `sudo systemctl [enable|disable] ssh`   
   
   
- Server config file: `/etc/ssh/sshd_config`   
- Client Config file: `/etc/ssh/ssh_config`   
   
### Check status   
   
   
- `systemctl status ssh` or `systemctl status sshd`(for CentOS)   
- `ps -ef | grep sshd` can   
- `systemctl is-enabled ssh` to start at boot   
   
### Troubleshooting ssh   
   
### Connecting to ssh server   
   
   
- Using [ping](../devlog/ping.md) to test connection between either ssh server or client   
  - `ping IPAddr` see: [Troubleshooting for connectivity issues](../devlog/troubleshooting%20for%20connectivity%20issues.md)   
- Connecting using a client(OpenSSH)   
  - `ssh username@serverIPAddr` or `ssh -l username IPAddr`   
  - The username used should exist on the server, not on the client   
- The first time whena client is connecting to an ssh server, the client uses a cryptographic fingerprint to identify the server and prevent possible man in the middle attacks in the future.   
- The host key is randomly generated when the ssh server is set up and is used to identify the server you're connecting to.   
- It will be saved on the client in the file called [/.ssh/known_hosts](/not_created.md)   
- You'll be prompted to enter the user's password, press enter to start your connection.   
- To exit, run `exit` or `Ctrl + D`   
   
### Options   
   
   
- To use a port other than the default one(Port 22) use `-p` followed by the port number.   
- ssh client has it's own configuration file under ``/etc/ssh/ssh_config`   
   
check out: [putty](https://www.putty.org/)   
   
### Securing SSH with Key Authentication   
   
   
- Use [ssh-keygen](../devlog/ssh-keygen.md) to for Public Key Authentication   
- Disable password authentication of the remote machine   
  - `vim /etc/ssh/sshd_config`   
  - Make `PasswordAuthentication no`   
  - `systemctl restart ssh`   
   
### Troubleshooting [ssh](../devlog/ssh.md)   
   
The first to check is that the ssh daemon is running on the server machine:   
`systemctl status ssh`   
   
If you get a `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!` message on the client when trying to connect/autheticate ssh server, double check that you're connecting to the right server. This message will be displayed if the [ip address](../devlog/ip%20address.md) or [MAC](../devlog/mac.md) Address have been changed. If it is the right server, you can get rid of the message by removing the server key from the `/.ssh/known_host` file.   
   
Check [Port 22](/not_created.md) on which the server listens is open, from the client scan the Port 22 on the server. Use [telnet  protocol](../devlog/telnet%20%20protocol.md)) or [Nmap](../devlog/nmap.md) for this.   
   
   
- `telnet IPAddr PortNumber(22)`   
- `nmap -p 22 IPAddr`   
  - If it returns saying, "Host seems down" add the `-Pn` options and run again to get if the [Port 22](/not_created.md) is open or not.   
   
Check if there is a [firewall](../devlog/firewall.md) dropping the packets.   
The Linux firewall is called [netfilter](/not_created.md) or [iptables](/not_created.md).   
To check if there are any firewall rules by running; `sudo iptables -vnL`   
If you suspect a firewall issue then use [ufw](../devlog/ufw.md).   
   
See also: Securing the [OpenSSH](/not_created.md) Server ([SSHD](../devlog/sshd.md))