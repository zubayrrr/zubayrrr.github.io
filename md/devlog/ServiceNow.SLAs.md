---
created: 1665628423440
desc: ''
id: me5ohp3wcp2t5r20yt3q5p0
title: SLAs
updated: 1665628423440
---
   
## Service Level Management   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665504243/wiki/g5zmxs2l3lstmpkkumrd.png)   
   
## Service Level Agreements   
   
> “A service level agreement (SLA) is a record that specifies the **time** within which **service** must be provided.” — ServiceNow Docs   
   
   
- They define time periods or windows of when certain records such as an Incident must meet a promised deadline.   
- They’re used to track if a certain level of service(previously promised) is being provided/has been provided.   
- They’re most commonly used for [ServiceNow.Incident](../devlog/ServiceNow.Incident.md)s but may also be used for other records in the system.   
- They can leverage [ServiceNow.Workflows](../devlog/ServiceNow.Workflows.md) which is a powerful tool used to define processes in ServiceNow.   
- SLAs consists of Start, Pause, Stop and Reset conditions. These conditions define what that window of time (SLA) looks like.   
- Time zones, business calendars and duration plays a crucial role in defining quality SLAs.   
- They also have a retroactive start feature, which allows the system to trigger the start of an SLA based on different events and fields such as the “updated” vs “created” fields.   
   
## SLA Definitions   
   
This is where we define SLAs in the system.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665505763/wiki/mwl8mcbmdns9du5viyse.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665505847/wiki/dgb2p8l0euumbz0f5glg.png)   
   
When we create a new “Priority 1” Incident created in the Incident table, it will start an SLA definition and it will continue to run until it hits any other conditions(pause, stop, reset).   
   
Out of box, there is a period of time where a “Resolved” incident that automatically goes to a “Closed” incident state. This is a measure to ensure that an incident really is resolved. Example: The service desk technician might resolve it before the SLA reaches it’s critical time(resolution time) but the Caller may come back and report a different state. The stop condition only sets in when the incident state is “Closed”.   
   
## SLA Workflow   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665506291/wiki/o0wkvpmymdfd8ek6ckpw.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665506520/wiki/ofjt3jmduvraafedhnhz.png)   
   
## Type: Underpinning contract   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665506700/wiki/fidk6i8liuwdfu9wibdl.png)   
   
If an contract is associated with this Configuration Item. This contract may be a vendor that supports this CI so we may hold that vendor accountable for this incident.   
   
For example: Let’s create an incident with CI as “Storage Area Network” as defined in the above SLA definition and make it “Priority 1” SLA.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665507076/wiki/n7eb7h2ov7mqzkghogdg.png)   
   
This will create two SLAs as it qualifies for two different SLA definitions.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665507192/wiki/zxa0os1pf2ea9pakdobk.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665507281/wiki/xh018sp7ruvrp9pckryl.png)   
   
Get additional information on a specific SLA by opening it’s record.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665507323/wiki/vgyitnxnfakoctakuwxa.png)   
   
You can also open the SLA’s workflow context and view it’s timeline.   
   
Try to trigger their Pause, Stop conditions by setting the incident state to whatever the conditions expect and watch the SLA’s state get changed.   
   
If an incident is not resolved/closed in the SLA defined time(Priority 1), we’d have “Failed” the SLA but other SLAs attached to that incident would work respectively.   
   
See also: [ServiceNow.OLAs](../devlog/ServiceNow.OLAs.md)