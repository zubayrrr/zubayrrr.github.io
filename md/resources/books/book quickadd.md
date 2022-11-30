---
category: <% tp.file.creation_date("YYYY") %>
created: <% moment(tp.file.creation_date("YYYY-MM-DDTHH:mm:ss.SSSZ")).toISOString()
  %>
id: <% tp.user.new_uuid() %>
tags:
- books
title: <% tp.file.title %>
updated: <% moment(tp.file.last_modified_date("YYYY-MM-DDTHH:mm:ss.SSSZ")).toISOString()
  %>
---
   
Title:: {{VALUE: What’s the actual book title?}}   
By:: {{VALUE: Who’s the author(s)?}}   
Topics:: {{VALUE: What’s the topic?}}   
Related:: {{VALUE: Is this related to any other notes?}}   
Status:: {{VALUE:#read,#unread,#partially-read}}   
   
   
---