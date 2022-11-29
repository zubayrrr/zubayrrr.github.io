---
created: 1656060995650
desc: ''
id: 9zyk7wwcwwwx1bi9pxy7e82
title: Bastion Host
updated: 1656061276021
---
   
A Bastion Host/Server is used to manage access to an internal or private network from an external network. It is also known as a Gateway Server or a Jump Box or a Jump Server.   
   
It basically helps with security - monitoring incoming and outgoing traffic. Bastion Host has clear user rules defined; who can access what.   
   
User will first sign into Bastion Host and get validated and proceed with SSHing into other machines. If we want to cut off all the external access to our internal servers, all we'd have to do is destroy the Bastion Host.