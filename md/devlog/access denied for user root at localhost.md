---
created: 20211104223035710
desc: ''
id: z6st1cdnl60ecoyrkrw06ng
tags:
- tidbits
title: Access denied for user 'root'@'localhost'
updated: 1653304922224
---
   
Topics::  [languages.sql](../devlog/languages.sql.md)   
   
`sudo mysql`   
   
or   
   
Add switch -p for password based login:   
   
`mysql -u root -p`   
   
`SELECT user,authentication_string,plugin,host FROM mysql.user;`   
   
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Current-Root-Password';FLUSH PRIVILEGES;`   
   
## OR   
   
`INSERT INTO mysql.user (Host, User, Password) VALUES ('%', 'root', password('YOURPASSWORD')); GRANT ALL ON *.* TO 'root'@'%' WITH GRANT OPTION;`   
   
`sudo mysql -u root -p`