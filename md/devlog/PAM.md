---
created: 1665628422982
desc: ''
id: yfj1glgwsmpaoalvrodbp7g
title: PAM
updated: 1665628422982
---
   
Because administrator accounts have elevated privileges that can access valuable data and execute applications or transactions—often with little or no tracking control—it can be very difficult to manage privileged accounts. PAM solutions centralize management of administrator profiles and ensure [least privilege access](https://www.coresecurity.com/blog/what-does-least-privilege-access-actually-mean) is enforced to give users only the access they need.   
   
While [IAM](../devlog/IAM.md) and [IGA](../devlog/IGA.md) focus on wider levels of user access for resources, systems, and applications across the organization, PAM primarily defines and controls access for privileged users.   
   
### What Are Privileged Accounts?   
   
Privileged accounts are typically shared accounts that inherently possess elevated access to data or services. In more vivid terms, these accounts are considered elevated accounts within your IT environment that hold the 'keys to the kingdom.' Examples of elevated privileges include the ability to change system configuration, to install or remove software, or to add, remove or modify user accounts. Elevated privileges can also just simply be access to sensitive data. Below are three specific types of privileged accounts:   
   
   
- **Root/Administrator Accounts**: These accounts possess full authority to systems and have no restriction for accessing services or data residing on a server. They are considered the most valuable targets for threat actors.   
   
   
- **System Accounts**: These accounts are used for running operating system services and can modify the relevant files and configurations. They are typically provisioned with the operating system.     
   
   
- **Service/Application Accounts**: These accounts are used for running processes and applications through automated, often unattended tasks. They frequently own or have access to data, resources, or configurations not available to non-privileged users.