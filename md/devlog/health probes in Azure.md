---
category: '2022'
created: 2022-12-05 19:04:49.810000+00:00
id: 9ab9bc83-596b-4a6c-a0dc-1e2178b2f2ca
tags:
- devlog
title: Health Probes In Azure
updated: 2022-12-05 19:04:50.486000+00:00
---
   
Topics:: [Azure](../devlog/Azure.md)   
   
   
---   
   
In Azure, health probes are used to monitor the health and availability of virtual machines, web apps, and other resources. Health probes use a protocol to check the health of a resource, and to determine whether it is available and responsive.   
   
The following protocols are available for configuring health probes in Azure:   
   
   
-   [HTTP](../devlog/http.md): used to check the health of a web app or other HTTP-based resource. The probe sends an HTTP request to the resource, and checks the response to determine whether the resource is healthy.   
-   HTTPS: used to check the health of a web app or other HTTPS-based resource. The probe sends an HTTPS request to the resource, and checks the response to determine whether the resource is healthy.   
-   [TCP](../devlog/TCP.md): used to check the health of a network connection or other TCP-based resource. The probe establishes a TCP connection to the resource, and checks the connection to determine whether the resource is healthy.   
-   [PING](../devlog/ping.md): used to check the health of a network connection or other resource that supports the PING protocol. The probe sends a PING request to the resource, and checks the response to determine whether the resource is healthy.