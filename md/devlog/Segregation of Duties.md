---
created: 1665628423002
desc: ''
id: yhfgxyhi3r0bjdcb48g069t
title: Segregation of Duties
updated: 1665628423002
---
   
The increasing reliance of business processes on the IT systems supporting their execution highlights the risks arising from the lack of proper segregation of duties (SoD) resulting from granting employees with excessive system authorizations, inadequate to their official duties. Planning for an appropriate division of responsibilities and reflecting it in the access privileges granted to users of IT systems becomes necessary for the proper, efficient and secure execution of the business processes.   
   
It is important to prevent members of an organization from gaining operational privileges that might cause conflicts of interest that can be detrimental to the organization.   
   
You must establish **constraints** when you assign **entitlements** to users.   
   
Segregation of duty (SoD) mechanisms are designed to manage conflicting relationships between certain model entities. Entities that are characterized by reciprocal conflict, cannot be aggregated to the same user.   
   
Most of the existing models for SoD show that conflicts are defined based on permissions and roles.   
   
Defining conflicting roles can lead to inconsistent results.   
   
For example, an organization has three roles, R1, R2, and R3. Two of these roles, R1 and R2, are defined as conflicting.   
   
If R2 and R3 are built with the same permissions, then both pairs (R1, R2) and (R1, R3) would give the user access to conflicting permissions. Basically R2 is equivalent to R3, even though, by definition, only the pair (R1, R2) can be considered as conflicting roles.   
   
According to the [RBAC](../devlog/RBAC.md) model, roles are containers of groups of permissions; the user's actual operating capacity depends on the permissions that define the operational characteristics of a role.   
   
In the previous example, one method is to redefine the conflicting permissions. The conflict between roles is caused by the conflicting permissions.   
   
In large organizations, IT systems can register hundreds of thousands of permissions. Redefining permissions is impractical.   
   
[Segregation of Duties (SoD): a specific type of Risk - IBM Documentation](https://www.ibm.com/docs/en/sig-and-i/5.2.1?topic=model-segregation-duties-sod-specific-type-risk)