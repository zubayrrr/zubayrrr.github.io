---
aliases:
- ServiceNow.Self-Service
- Self-Service
category: '2022'
created: 1665673647258
desc: ''
id: 9da20d17-b287-442a-b082-ab3f02dfea52
title: Self-Service
updated: 1665673647258
---
   
## Self-Service Application   
   
   
- Accessible by every user in ServiceNow   
- Does not require a role   
* Personalized information   
* Contains a lot of sub-modules(list like) that are **specific to you**(the current user).   
* Typically, service now customers will use [ServiceNow.Service Portal](../devlog/ServiceNow.Service%20Portal.md) to display information about the user instead of relying on Self-Service   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665673754/wiki/gusmal6rs1su6fqqcbgh.png)   
   
   
## Dashboards   
   
   
- Dashboards are the new homepages     
- May contain reports, and dashboard widgets     
- Any user may create a new dashboard   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665673790/wiki/pi3dyzcey174eh9buhgi.png)   
   
Create a new Dashboard   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665674841/wiki/ipdjtiyc3prcnxx0l0tt.png)   
   
Once created, you can add widgets to your dashboard.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665674908/wiki/ropj64ixsz2v0b8khuv5.png)   
   
   
## Misc   
   
   
- Business Applications   
- [ServiceNow.Service Catalog](../devlog/ServiceNow.Service%20Catalog.md)   
- [ServiceNow.Knowledge](../devlog/ServiceNow.Knowledge.md)   
- Help the Help Desk   
- [ServiceNow.Visual Task Boards](../devlog/ServiceNow.Visual%20Task%20Boards.md)   
- (My) Incidents   
- Watched Incidents (When you’re in the watchlist for the incident)   
- My Requests   
- Requested Items   
- etc   
   
The applications(modules) listed on your Self-Service menu really depends on what roles have been assigned to you, for example you won’t have access to **My Approvals** application unless you’ve the role `approver_user`   
   
Details on what application requires which role can be found under **System Definition** → **Application Menus**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665674509/wiki/wdij5szh4bvz3qqbk3nn.png)