---
created: 1665628082230
desc: ''
id: ycsmk80ngm5eqatq1goosok
title: Change
updated: 1665628082230
---
   
> “The objective of change management in this context is to ensure that **standardized methods** and **procedures** are used for efficient and prompt handling of **all changes** to control IT infrastructure, in order to **minimize** the number and impact of any related incidents upon service.”   
   
A change is an event that is approved by the management and implemented with a minimized and accepted risk to the existing IT infrastructure, results in a new status of one or more configuration items and provides increased value to the business from the use of the new/enhanced system.   
   
   
- There are 3 types of change:   
  - Normal   
    - A typical change, raised through an RFC, reviewed by CAB (Change advisory board), rejected or approved by change manager.   
  - Standard   
    - Pre-approved, performed frequently, relatively risk free. Typically not tracked as a “request for change” (RFC).   
  - Emergency   
    - A change that must go in effect ASAP. The review of such changes happen after the fact. Examples: security patch.   
- A change is a record in `change_request` table.   
- Changes can be quite complex that has a lot of moving parts.   
   
## Change Management   
   
   
- There are risks assessments that try to calculate what the risk looks like.   
- Out of box there are workflows for all kinds of changes.   
- Out of box [ServiceNow.Service Catalog](../devlog/ServiceNow.Service%20Catalog.md) for change proposal.   
- Schedules for changes.   
- Calculated risks - changes touching upon same configuration item carry some amount of risks to them.   
   
## Change Application   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665519261/wiki/kl8ty2pkprq6nexl6gby.png)   
   
## Create New   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580028/wiki/bu4yjduuxqb09h4zfivc.png)   
   
## Standard Change   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580088/wiki/vxtbtg8tncljemhuwxe4.png)   
   
Choose a template to auto-populate fields   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580153/wiki/zepvmsmsoxbvurc8spev.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580197/wiki/ohz5vyc1aid7nsdnrjbk.png)   
   
## CAB   
   
CAB Workbench Calendar showing all the CAB meetings. You can go inside a meeting to find additional information such as the changes associated with a CAB meeting.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580468/wiki/rxyymavsja9fgsrkwlpy.png)   
   
## Schedules   
   
Change schedules that an organization defines.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580688/wiki/xut8ffajs36s7742je9m.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580784/wiki/it7t87v6k5bkzpmhbswx.png)   
   
## Administration   
   
### Change Properties   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580863/wiki/t1vzgmn1ksuklkvsclxd.png)   
   
### Risk Conditions   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665580995/wiki/p6ihz5reaka053divbpx.png)   
   
### Blackout Schedules   
   
Will not allow changes to happen on specified dates.   
   
## Misc   
   
   
- Change tasks are generated on the Implement stage.