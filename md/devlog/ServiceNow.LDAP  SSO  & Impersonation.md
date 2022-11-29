---
created: 1663417541082
desc: ''
id: 8ihtgsdgow6oadome4santb
title: LDAP  SSO  & Impersonation
updated: 1663418089606
---
   
   
   
- Lightweight Directory Access Protocol, operates on Port 389   
- Open, vendor-neutral, industry standard for accessing and maintaining distributed directory information services.   
- LDAP and Active Directory use this port.
   
   
An LDAP integration is used to authenticate users and populate users & groups in ServiceNow.   
The integration is read-only, ServiceNow cannot modify the company's LDAP system.   
   
There are 2 parts to this integration:   
   
   
- Authentication   
- Data Population   
   
If an LDAP integration is successfully configured between ServiceNow and LDAP software, the users can access their ServiceNow accounts by using their LDAP credentials.   
   
Data population is used to populate user and group data from LDAP service. It makes maintaining user and group data much easier.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663419791/wiki/et9mnwuee8bs7d5fayur.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663419822/wiki/ej2zgsqc21bliun5kvmn.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663419833/wiki/jkehz9zyag9op7tnnxyl.png)   
   
   
## SSO   
   
Single Sign-On   
   
   
- It is used for authentication.   
- Basically, it enables users to have one set of credentials for all applications across their organization.   
- There are 3rd party providers for SSO and is much secure.   
- ServiceNow has different configuration types including SAML 2.0 and OpenID.   
   
SSO integration comes as a plugin in ServiceNow    
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663420005/wiki/omit4jbtqdyh6ztzu8jj.png)   
   
Activate it   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663420083/wiki/a92bmcls9cryfncksspr.png)   
   
   
## Impersonation   
   
Administrators can impersonate other authenticated users for testing purposes and view impersonation logs.   
   
Only the user with **admin** or **impersonator** role can impersonate users.   
   
When impersonating another user, the administrator has the exact access as the impersonated user. As if that user is currently logged in.