---
created: 1665628422960
desc: ''
id: 4fymfbnov6h310xtehsuxi2
title: IdentityNow
updated: 1665628422960
---
   
It is a comprehensive [IGA](../devlog/IGA.md) solution. It is a fully stacked solutions that cover all aspects of identity lifecycle management. It is a multi-tenant, microservices based SaaS. Furthermore, it maintains a single code-base. All customers are on the same version of SailPoint IdentityNow. It is not a hosted on-prem solution. It manages both on-prem and cloud applications.   
   
It was designed with the end-user in mind, it is a self-service platform that makes complex [IGA](../devlog/IGA.md) tasks understandable and user-friendly(to business users).   
   
With IdentityNow, you see all users and their access in one place.   
   
## High-level Overview of IdentityNow   
   
Your enterprise(on-prem and cloud), it may include DBs and Directories, HR systems, SSO solutions, IAM solutions, PAM solutions, ITSM solutions.   
   
IdentityNow’s capabilities are powered by 32 microservices.   
   
It can do things like:   
   
   
- Provisioning   
- Access request    
- Access certification   
- [Segregation of Duties](../devlog/Segregation%20of%20Duties.md)   
- Password management   
- Cloud Platform Services provided by SailPoint Hosted Administrators   
	- Scaling   
	- Alerting    
	- Monitoring   
- Platform Extensions   
	- File Access Management (unstructured data)   
		- Visibility    
		- Ownership   
		- Apply Access Controls   
	- Intelligent Insights   
		- by Identity AI    
   
The entry point inside IdentityNow is an integration framework made up of connectors, RESTful APIs and deep product integrations.   
   
 **IdentityNow Virtual Appliance(s)**.The glue connecting an enterprise to IdentityNow is a secure gateway, a virtual appliance deployed within your infrastructure.   
   
Instead of dealing with complicated firewall rules, the virtual appliance only communicates OUTBOUND to IdentityNow using zero knowledge encryption.   
   
## Onboarding   
   
Users can be created from an HR system or other systems and connect them to IdentityNow and it will automatically discover the user and start the **“Provisioning”** process. IdentityNow will use attributes like kinda of employee, location, reporting, job title, department to automatically grant **Birthright Access** on day 1.   
   
## Birthright Access   
   
Birthright access **grants an employee what they need based on who they are and what they do within an organization**. In other words, this is the standing access an employee has. It's their “birthright”, just by existing.   
   
## Access   
   
**Identity Cube**   
   
> Identity Cube (n): All of the information associated with an identity, including all of their accounts on all sources, all attributes and entitlements of those accounts, as well as IdentityNow attributes and entitlements such as the lifecycle state and SailPoint status.   
   
**My Access** — as per the roles, entitlements many accounts for different services will be created automatically. The entitlements will be associated with those different accounts(like permissions to take certain actions in Active Directory) .    
   
**Roles** are assigned as per the attributes. The flexibility of the roles associated can be tailored to business requirements.   
   
**Access Profiles** are more specific to individual application such as Active Directory etc.   
   
**Applications**    
   
A high level of different accounts for different end-point systems. Access to applications based on different group membership.    
   
## Request Center   
   
 Used to request discretionary level of access of systems. To process one-off requests.   
   
## Connected Sources   
   
In IdentityNow connected sources are basically having a connection directly with the target sources or the applications. They can provision accounts, objects or user accounts directly while taking to the application or the source without any human intervention with the help of certain rules and policies which are set.   
   
## Disconnected Sources   
   
Sources that do not allow to connect through IDN. There is a need for manual process when provisioning of the user account into the application. No track-ability and visibility of the process.   
   
## Links   
   
   
- [IdentityNow.Glossary](../devlog/IdentityNow.Glossary.md)   
   
## Resources   
   
   
- [Improve Compliance and Efficiency with IdentityNow - YouTube](https://www.youtube.com/watch?v=nAvHTQT2f8U)   
- [ENH iSecure Overview Of IdentityNow - YouTube](https://www.youtube.com/watch?v=NH7yQlYcNmc)   
- [ENH iSecure Overview Of IdentityNow Demo - YouTube](https://www.youtube.com/watch?v=MJR5LJacaik)   
- [Leverage SailPoint and ServiceNow to Improve the User Experience and Reduce Risk Through Automation - YouTube](https://www.youtube.com/watch?v=eip-xwfxe5w)   
- [ServiceNow Workflow || Group Management || Part 1](https://www.youtube.com/watch?v=sD7hx--Ud48)   
- [Sailpoint training | Sailpoint tutorial for beginners | Sailpoint Tutorial | Sailpoint course - YouTube](https://www.youtube.com/watch?v=r9k2w5CnKcY&t=221s)   
- [IdentityNow Architecture | Learnings :)](https://tanaychouhan.wordpress.com/2020/07/27/identitynow-architecture/)