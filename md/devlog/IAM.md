---
created: 1665628081738
desc: ''
id: 52tr7f9tkivmqwzttra84lm
title: IAM
updated: 1665628081738
---
   
##  Identity and Access Management   
   
Identity and Access Management (IAM) is an advanced security structure for business processes, policies, and technologies that helps organizations to manage electronic/digital identities of workforce & customers”. With an IAM structure in place, IT admin can make certain that the right people (Organizational employee, end-user) can access the tools they need to do their daily grind. Simply stating, based on the individual role defined, they will get access to a set of application resources. For illustration, in an Organization, the account team will get access to all resources related to accounting and finance while sales and marketing will get access to the marketing-related tools to work on. Therefore, IAM Implementation eases the efforts of admins by automating it to manage roles, identity, and access of each user individually without logging into each app as an administrator.   
   
In addition to identity management and access management, multiple security technologies and tools are used in IAM to maintain the security, integrity, and confidentiality of the organization. These include technologies like Single Sign-on([SSO](../devlog/SSO.md)), Two-factor authentication/multi-factor authentication, Adaptive Multi-Factor Authentication, and Provisioning. These all mentioned IAM technologies let organizations securely store identity and profile data as well as data governance functions to ensure that only data that is necessary and relevant is provided.   
   
Primarily, IAM encircles the following aspects:   
   
   
- **How users will be identified** in a system   
- Based on the identified user **how roles will be defined** in a system and how it will be assigned to each individual   
- **Adding, Removing, and Updating users roles and access** levels in a system   
- Assigning **different levels of access** to users based **on groups and roles** defined for the individual   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665436230/wiki/zkuvznpuisqzqwhctakx.png)   
   
IAM systems provide these core functionalities:   
   
**User identity Management**   
   
The IAM system can also operate as a single directory that **creates, modify and delete users,** or it may integrate with one or more other directories (IDP, **[Azure AD](https://blog.miniorange.com/what-is-azure-active-directory/)**, **[LDAP](https://blog.miniorange.com/what-is-ldap/)**) and synchronize with them. Identity and access management can also create new specialized identities which demand high level access to an organization’s tools.   
   
**Authenticating users**   
   
IAM systems **authenticate a user by confirming that they are who they state they are to be** (Username and Password). Today, secure authentication means **[multi-factor authentication (MFA)](https://blog.miniorange.com/what-is-multi-factor-authentication-mfa/)**, **[Passwordless Authentication](https://blog.miniorange.com/passwordless-authentication/)**, and adaptive **[authentication](https://www.onelogin.com/learn/what-why-adaptive-authentication)**.   
   
**Authorizing users**   
   
**Access management ensures a user is granted the exact level and type of access** to the resources they’re entitled to. Users can also be grouped based on roles so that a large number of users can be granted similar privileges.   
   
**Provisioning/Deprovisioning users**   
   
**Permitting access to resources based on roles defined (publisher, editor, viewer, commenter) to an individual is called** **_provisioning_**. IAM tools allow admins to provision users by their role, field, or another specific group to which they belong. Since it is time-consuming to manage and specify each individual’s access to every resource manually, identity management systems enable provisioning via policies defined based on role-based access control. Users are assigned one or more roles, usually based on job function, and the IAM system automatically grants them access. Provisioning also works in reverse (**[Deprovisioning](https://www.miniorange.com/user-provisioning)**); to avoid security risks presented by ex-employees retaining access to systems, IAM allows your organization to quickly remove their access.   
   
**Single Sign-On**   
   
Identity and access management solutions with **S\*\***ingle Sign-On (SSO)\*\* **provide a unified platform to authenticate user identity instead of many different resources**. Once authenticated, the IAM system acts as the source of identity truth for the other resources available to the user, removing the need for the user to remember multiple passwords.   
   
**Reporting & Auditing**   
   
IAM tools **generate timely reports after most actions are taken on the platform (like login time, systems accessed, timestamp, unique user count, and type of authentication) to warrant compliance needs and access security risks, if any.**   
   
[What is Identity and Access Management (IAM)?](https://blog.miniorange.com/what-is-iam-identity-and-access-management-system/)   
   

   
# Authentication Vs Authorization   
   
or   
   
# Identity management Vs Access management   
   
   
---   
   
## Authentication or AuthN   
   
**Authentication verifies the identity of a user or service**   
   
**_Identity management_** confirms that you are you by authenticating and storing information about you. An identity management database holds information about your identity – for example, your job title, stream and authenticates that you are, indeed, the person described in the database.   
   
## Authorization or AuthZ   
   
**Authorization determines their access rights**   
   
**_Access management_** uses the info about your identity to determine which resources you’re allowed access to and what you’re allowed to do when you access them. For example, access management will ensure that every employee within the Finance group has access to all related apps for payment processing and data analysis, but not so much access that they can do confidential banking.   
   
[What is Identity and Access Management (IAM)?](https://blog.miniorange.com/what-is-iam-identity-and-access-management-system/)
   
   
See also: [IGA](../devlog/IGA.md), [BYOI](../devlog/BYOI.md), [BYOD](../devlog/BYOD.md)