---
aliases:
- ServiceNow.Integrations
- Integrations
category: '2022'
created: 1666124833487
desc: ''
id: 63404566-1e46-41cf-b91f-677a32925804
title: Integrations
updated: 1666124833487
---
   
Integrations are used to transfer information from one system to another, to establish communication — this can be uni-directional or bi-directional.   
   
## REST Integrations   
   
ServiceNow can send [REST API](../devlog/REST%20API.md) calls to system and accept calls back from other systems.   
   
REST is a set of rules and the underlying communication is happening based on the [http](../devlog/http.md).   
   
   
**Basic Building Blocks** of a REST integration:   
   
   
- Endpoints   
	- Reference to URI which accepts web requests; **where to send the data**   
- Methods   
	- **Action to perform**; GET, POST, PUT, PATCH, DELETE etc   
- Authentication    
	- **Who is sending the data, are they allowed to do so?**   
- Content/Body   
	- [XML](/not_created.md)/ [JSON](/not_created.md)   
- Content Type   
	- Data    
   
**How does a REST call work?**