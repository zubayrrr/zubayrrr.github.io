---
created: 1656340408552
desc: ''
id: x2xmqg7ehbnyfhec51ptojw
title: Localhost
updated: 1656340679744
---
   
When you call an IP address on your computer, you try to contact another computer on the internet but when you call the IP address 127.0.0.1 then you are communicating with the local host. Localhost is always your own computer. Your computer is talking to itself when you call the local host. Your computer does not always directly identify the local host. Within your personal network localhost has a separate IP address like 192.168.0.1. (for most cases) which is different from the one you use on the internet. This is usually dynamically assigned by the internet service provider (ISP). Localhost can be seen as a server that is used on your own computer.   
   
This term is generally used in the context of networks. Localhost is not just the name for the virtual server but it is also its domain name. Just like .example, .test, or .invalid, ., .localhost is a top-level domain reserved for documentation and testing purposes. While accessing the domain, a loopback is triggered. If you access “...quely assigned in it, as is usually the case. Also, it was reserved by ICANN.   
   
If you enter an IP address or corresponding domain name in your browser, the router forwards your request to the internet which connects you to the server. This means that if you enter 172.217.0.0, you will reach the Google homepage but the situation is different with 127.0.0.1. The requests to this address will not be forwarded to the internet. [tcp⁄ip model](../devlog/tcp%E2%81%84ip%20model.md) recognizes from the first block (127) that you don’t want to access the internet, you are calling yourself instead. This then triggers the loopback.   
   
The reason why a loopback device is created is so that the backlink to your own computer works. Through the operating system, this is a virtual interface that is created. The interface is called lo or lo0 and can also be displayed using the [ifconfig](../devlog/ifconfig.md) command in Unix systems. A similar command for Windows is ipconfig. — via [What is Local Host? - GeeksforGeeks](https://www.geeksforgeeks.org/what-is-local-host/)