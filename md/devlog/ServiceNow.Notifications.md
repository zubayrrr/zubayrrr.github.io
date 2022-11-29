---
aliases:
- ServiceNow.Notifications
- Notifications
category: '2022'
created: 1665681755104
desc: ''
id: 1f32e548-d3a5-40dd-9e68-5f036d4dc300
title: Notifications
updated: 1665681755104
---
   
   
- ServiceNow supports email and SMS notifications.   
- Notifications are often triggered by events.   
	- For example: “assigned to”    
- ServiceNow provides templates for injecting variables in existing HTML templates.   
   
Event name: `notification_engine.process` tells that a notification was processed.   
   
See: **System Logs** → **Emails**    
Email Log Entry   
   
**Push** is for SMS   
   
See also:  **System Notifications** → **Emails** → **Notifications** to list all the configured system notifications.   
   
Use Notifications to notify users about specific activities in ServiceNow, such as updates to incidents or change requests. Notifications allow administrators to specify     
   
   
-   When to send the notification   
-   Who receives the notification   
-   What content is in the notification   
   
Notifications can be sent (if the specified **Conditions** are met) under one of the following circumstances:   
   
   
-   A record is **Inserted** or **Updated** into the **Table** specified above   
-   The specified event is fired   
-   Via a Flow Action   
   
Notifications can be sent to specific **Users** and **Groups** or to **User/Groups in fields** on the record that generated this notification.   
   
If using an **Email Template** then **Subject** and **Message** will be used from the template unless overridden with a **Subject** and **Message** on this form.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665681734/wiki/z5s4z0gxweekjnh48vcy.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665681912/wiki/ebm0mkllgws3wlos3tty.png)   
   
You can also choose parameters( like recipients ) in the notification configuration.   
   
Message Templates = Email Scripts defined in the **Notification Email Scripts** module.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665682330/wiki/arj4jzvrz6iyduy5mysc.png)