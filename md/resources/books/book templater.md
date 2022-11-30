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
   
Title:: <% await tp.system.prompt("What’s the actual book title?") %>   
By:: <% await tp.system.prompt("Who are the authors?") %>   
Topics:: <% await tp.system.prompt("What are the topics?") %>   
Related:: <% await tp.system.prompt("Related Links") %>   
Status:: <% await tp.system.suggester(["#read", "#unread", "#partially-read"], ["#read", "#unread", "#partially-read"]) %>   
   
   
---