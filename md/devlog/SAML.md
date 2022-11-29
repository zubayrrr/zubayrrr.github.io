---
created: 1665628422996
desc: ''
id: 6vedfmgz7h3pydfxaly5e91
title: SAML
updated: 1665628422996
---
   
*SAML* is an acronym used to describe the Security Assertion Markup Language (SAML). Its primary role in online security is that it enables you to access multiple web applications using one set of login credentials. It works by passing authentication information in a particular format between two parties, usually an identity provider ([idP](../devlog/idP.md)) and a web application.   
   
## What SAML is and How it Works   
   
SAML is an open standard used for authentication. Based upon the Extensible Markup Language (XML) format, web applications use SAML to transfer authentication data between two parties - the identity provider ([IdP](../devlog/idP.md)) and the service provider (SP).   
   
The technology industry created SAML to simplify the authentication process where users needed to access multiple, independent web applications across domains. Prior to SAML, single sign-on ([SSO](../devlog/SSO.md)) was achievable but relied on [cookies](../devlog/cookies.md) that were only viable within the same domain. It achieves this objective by centralizing user authentication with an identity provider. Web applications can then leverage SAML via the identity provider to grant access to their users. This SAML authentication approach means users do not need to remember multiple usernames and passwords. It also benefits service providers as it increases security of their own platform, primarily by avoiding the need to store (often weak and insecure) passwords and not having to address forgotten password issues.   
   
[SAML Explained in Plain English | OneLogin](https://www.onelogin.com/learn/saml)