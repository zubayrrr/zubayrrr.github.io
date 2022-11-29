---
created: 1663331879336
desc: ''
id: xtf4ii3v4b61rvonda8vojd
title: Update Sets
updated: 1663332315097
---
   
Update sets are used to record most customizations and configurations.   
   
They’re used for moving changes from instance to instance.   
   
Everything in ServiceNow is stored as a record.   
   
They’re XML snapshot of latest modified record.   
   
They also have versions and you can merge two or more update sets into one.   
   
When you load an update set to an instance, you can preview the update set before committing the changes/customizations.   
   
Captured | Not Captured    
   
---------|----------   
 Customizations | Data, new records    
 Tables & Fields | Configuration items    
 Reports | Schedules   
 Workflows | Users   
 Forms | Groups   
   
[Customizations tracked by update sets](https://docs.servicenow.com/bundle/tokyo-application-development/page/build/system-update-sets/reference/customizations-tracked-update-sets.html)   
   
   
Click on “View current Update Set” button on the header will take you to the current Update Set record.   
   
In order to move an update from Development to Test or from Test to Production, you must set the state to “Complete”.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663332931/wiki/mvifpcnslpgk0tj5mblr.png)   
   
“Customer Updates” records represent modified customizations that were made in the platform in XML format.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663333027/wiki/kpbv3x3tae19tsenjsly.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663333153/wiki/krnfjehrgoklh4p5zeju.png)   
   
**Local Update Sets** are basically an Update Set that was created locally and is used to track the Update Sets as opposed to **Retrieved Update Sets** which will retrieve from another instance or imported as XML.   
   
**Create a new Update Set**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663333306/wiki/xiqwdxkbhnrsknl9a6gl.png)   
   
Any modifications in our system will be tracked by our newly created Update Set.   
   
## Update Sources   
   
We define a “source” to retrieve update sets from.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663333470/wiki/ysq4bygbx6wvkjfy85z0.png)   
   
Basically to retrieve update sets from other instance, whether they may be Test or Development or Prod.   
   
## Retrieved Update Sets   
   
Will display Update Sets retrieved from other instances or imported Update Sets with XML.   
   
When an Update Set is marked as complete, you’ve the ability to export it as XML to be imported eslewhere.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663333575/wiki/ouzofupsmz8qn9z99lga.png)   
   
## Update Log   
   
Shows the logs of the update sets committed.   
   
## Merge Update Sets   
   
Allows you to merge multiple Update Sets that are in state of “in progress”.   
   
## Merge Completed Sets   
   
Allows you merge multiple Update Sets that are in the state of “completed”   
   
## Update Sets to Commit   
   
A List view of Update Sets that are in loaded or preview state.   
   
   
You can specify an Update Set on records like Business Rules(basically customizations) to update them with the given Update Set – moving customer updates from one update to another.