---
created: 20211010131443024
desc: ''
id: l6mm6spmjonb3zpaca8nldg
title: Application Layer - OSI
updated: 1656562041903
---
   
# Layer 7 – Application Layer   
   
   
- Provides application level services (Not MS Word or Notepad)   
- Layer where the users communicate with the computer   
- Functions:   
  - Application services   
  - Services advertisement   
   
This layer grants a direct interface and access to the users with the network. The users can directly access the network at this layer. Few Examples of services provided by this layer include e-mail, sharing data files, FTP GUI based software like Netnumen, Filezilla (used for file sharing), telnet network devices etc.   
   
There is vagueness in this layer as is not all user-based information and the software can be planted into this layer.   
   
For Example, any designing software can’t be put directly at this layer while on the other hand when we access any application through a web browser, it can be planted at this layer as a web browser is using HTTP (hypertext transfer protocol) which is an application layer protocol.   
   
### Application Services   
   
Application level services in the [OSI Model](../devlog/osi%20model.md) context mean stuff like file transfer, the user communicates with the computer and the computer passes on the user request to the network.   
   
   
- Application services unite communicating components from more than one network application.   
- E.g:   
  - File transfers and file sharing   
  - E-mail   
  - Remote access   
  - Network management activities   
  - [Client](../devlog/client.md)/[Server](../devlog/server.md) Processes   
   
   
---   
   
### Service Advertisement   
   
   
- Some applications send out announcements   
- States the services they offer on the network   
- Some centrally register with the Active Directory server instead   
- E.g:   
  - Printer   
  - File Servers   
   
   
---   
   
### Layer 7 Examples   
   
   
- E-mail ([POP3](../devlog/pop3.md), [IMAP](../devlog/imap.md), [smtp](../devlog/smtp.md))   
- Web Browsing ([HTTP](../devlog/http.md), [HTTPS](../devlog/https.md))   
- Domain Name Service ([DNS](../devlog/dns.md))   
- File Transfer Protocols ([FTP](../devlog/ftp.md), [FTPS](/not_created.md))   
- Remote Access ([telnet  protocol](../devlog/telnet%20%20protocol.md)), [ssh](../devlog/ssh.md))   
- Simple Network Management Protocol ([SNMP](../devlog/snmp.md))