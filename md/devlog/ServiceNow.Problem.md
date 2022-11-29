---
created: 1665628082322
desc: ''
id: w52rd7dvxz40zpknqgfvtg1
title: Problem
updated: 1665628082322
---
   
> “The primary objectives of problem management are to **prevent** problems and resulting incidents from happening, to **eliminate recurring incidents**, and to **minimize the impact** of incidents that cannot be prevented.”   
   
Problem management is closely related to [Incident Management](../devlog/Incident%20Management.md).   
   
We use problem record to incident recurring incidents. It is also used to diagnose the root cause of a incidents identified through incident management process and to determine the resolution to those problems/incidents.   
   
   
- Problem records are stored in the problem table.   
- They may have related incidents displayed in the related lists in the problem form.   
- Problems may also have related Problem tasks. Think of them as steps that are need to resolve a problem properly.   
- We can also provide **Workarounds** for a problem to temporarily resolve a problem.   
   
## Problem Application   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516439/wiki/dokxknqmtfsdf3lgfv6s.png)   
   
### Create New   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516479/wiki/fuwvlrqsvrgwwtpqmqoh.png)   
   
## Problem Record(s)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516513/wiki/wjedvh212evu93gnegfv.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516548/wiki/pdihr6cd0qbn6sw20aw7.png)   
   
Incidents related to a problem are listed under “Related Links”   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516768/wiki/ydis9i6okpt15txzxmuf.png)   
   
You can add an existing incident to this list or a create one from scratch.   
   
## Problem Tasks   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516879/wiki/rijraf82mptlz4hlpaj3.png)   
   
Create a new Problem Task by clicking on the “New” button.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516937/wiki/smczhie1p18bwqodcwig.png)   
   
Select “General”   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665516991/wiki/gytjo9uw8qlhcrpgmw3m.png)   
   
Once created, it’ll appear in the Problem Tasks related list.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665517173/wiki/eg1uqb0jisvsibmzdcrd.png)   
   
You will also find links for:   
   
   
- Communicate Workaround   
- Communicate Fix   
- Post Knowledge   
- Post News   
   
Which basically enables you to notify any discoveries to all the related   
incidents of this problem. Or to generate a new knowledge article etc.   
   
You can also create a problem record from an incident form view.   
   
Once a problem is resolved, you can also resolve all the related incidents from the problem context menu.