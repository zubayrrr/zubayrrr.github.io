---
aliases:
- IdentityNow.Glossary
- Glossary
category: '2022'
created: 1665780492536
desc: ''
id: 5873c0b1-c226-4f20-b0f4-9844cc4ad4b2
title: Glossary
updated: 1665780492536
---
   
# Glossary   
   
## A   
   
**Access Modeling** (n): A SailPoint AI service, composed of Role Insights and Role Discovery, that makes the creation and maintenance of an organization's role model easy, fast, and relevant.   
   
**Access Profile** (n): A set of entitlements that represents a level of logical access (for example user, guest, admin, etc) to the source and/or a related app. With orgs that have Provisioning, access profiles are granted as part of provisioning actions. With orgs that do not have Provisioning, access profiles are used to determine if certain apps should be accessible to users based on whether they have all the entitlements included in the access profile.   
   
**Access Request** (n): (1) IdentityNow's Access Request service, which allows end users to request access that requires approval before it can be granted to users. (2) The access item assigned to a reviewer to approve or revoke when a user requests access using the Access Request service.   
   
**Access Request Recommendations** (n): Included in SailPoint's Recommendation Engine AI service. Suggests access to end users that they should request based on peer group analysis.   
   
**Access Request Approval Recommendations** (n): Included with the Recommendation Engine AI Service. Access request reviewers receive approval recommendations when reviewing access requests.   
   
**Account** (n): A user's access to a specific system of hardware or software either on-premises or on the web. This typically includes a unique identifier for the user, a unique password, a set of permissions associated with the system and some set of attributes. Accounts are loaded into IdentityNow through the creation of a source in IdentityNow.   
   
**Account Sync** (n): A configuration option in sources that support Provisioning that allows administrators to select identity attributes whose values can be copied over to related source attributes. This happens automatically at 12 hour intervals but an administrator can also manually synchronize the attributes of an individual identity from the identity's Accounts page using the Synchronize Attributes option.   
   
**Active Job** (n): These represent work being performed by IdentityNow. Aggregation is a common job.   
   
**Active Queue** (n): These represent the types of processes required to complete active jobs and the related items that are being processed in that queue. Example: Identity Processing   
   
**Admin** (n): Short for Administrator.   
   
**Administrator** (n): A person responsible for the technology management in a business. An administrator in IdentityNow has control over the system configuration, the applications, sources, and identities.   
   
**Admin Dashboard** (n): The front page of the Admin interface and the first thing admins see when they go to the admin-specific pages. Contains an overview of important system information.   
   
**Agg/Ag** (n): Short for Aggregation   
   
**Aggregate** (v): To gather and load user or entitlement data into IdentityNow from a source.   
   
**Aggregation** (n): The location and collection of information from the sources configured to work with IdentityNow. An aggregation gathers data and makes it ready to place in the identity cube.   
   
**Allow List** (n): A list of countries that your organization has deemed trustworthy. IdentityNow allows you to define security controls for any countries that do not belong to the allow list. Options include requiring strong authentication when launching certain apps.   
   
**API** (n): Application Programming Interface. Used by system administrators or external systems to request actions in IdentityNow without using the User Interface.   
   
**App** (n): Short for Application.   
   
**Application:** (n):   
   
1.  A generic term that refers to any data source SailPoint communicates with to manage governance, risk management and compliance for your enterprise.   
       
2.  An instance of a configured IdentityIQ connector. An application represents all the configuration and connection details required to connect IdentityIQ to a third-party system, for the purposes of governing and provisioning access to these systems. Details typically include how the target system is accessed (connection parameters), how the accounts and entitlement data on that system is classified (schema), and how the accounts on that system are correlated to existing Identity Cubes.   
       
   
**Approval** (n): The process of approving an Access Request.   
   
**Attribute** (n): A single item of data related to a particular user and the value contained in it. For example, a user's first name is an attribute.   
   
**Attribute Sync** (n): The process of synchronizing attributes from the identity cube to a target system. Useful for synchronizing attributes across different systems. For example, SAP and Active Directory or vice-versa.   
   
**Audit Report** (n): A report tracking administrator, user, and/or system actions within IdentityNow, found in Search.   
   
**Authenticate** (v): To verify your identity, usually via user name and password, and gain access to an account, application, or to IdentityNow.   
   
**Authoritative Source** (n): The primary source of employee information for your enterprise, such as a Human Resources application, used as the source of identities associated with a specific identity profile.   
   
## B   
   
**Beta** (n): Indicates a new set of functionality available to IdentityNow customers in which potentially any customer might have access. Users should be aware of the feature's limitations and work with their SailPoint contact to make suggestions or request assistance.   
   
**Birthright Access** (n): Access granted to a majority of identities just by becoming part of an organization. The granting of birthright access is usually triggered by a "start" event, such as first day on the job, moving to a new department, or a promotion.   
   
**Brand** (n): An identity attribute that is required for companies that need to support multiple color schemes and logos for identities that belong to their subsidiaries. Brand on the identity is associated with the Brand Identity Attribute on System Settings > System Customizations. Users of IdentityNow whose Brand attribute matches the value of the Brand Identity Attribute see the logos and colors specified for their brand.   
   
**Business Role** (n): In IdentityIQ, Business Roles generally represent job functions, titles, or responsibilities. They are usually tied to the organizational structure and are assigned to users based on their functions in the business – such as “Treasury Analyst” or “Accounts Payable Clerk”. Business roles define the desired state of a user’s access – what do we want someone with this job function to be able to do, or not do? Business roles are assigned to users directly: either automatically through attribute matching on things like job title or department, or through a request, which may come from the user himself or from someone else, like a manager or an application owner.   
   
## C   
   
**Campaign** (n): A set of certifications for all users or group of users, entitlements, and applications.   
   
**Campaign Filter** (n): A set of rules that defines the contents of a certification campaign.   
   
**Certification** (n): IdentityNow's mechanism for the approval or removal of entitlements for a user.   
   
**Certification Admin User** (n): A user in IdentityNow that has special permissions to create and manage certification campaigns.   
   
**Certification Recommendations** (n): Included with the Recommendation Engine AI Service. Access request reviewers receive approval recommendations when reviewing access requests.   
   
**Cluster** (n): A group of virtual appliances that are used to provide high-availability to the sources that are connected to them.   
   
**Connector** (n): The software that connects IdentityNow to a source system so that your data can be loaded into our identity governance system. See also: Source.   
   
**Correlation** (n): The process IdentityNow uses to determine whether a particular account belongs to an identity.   
   
**Current Profile** (on App) (n): The XML which defines the behavior and patterns of the app.   
   
## D   
   
**Delta Agg** (n): Short for Delta Aggregation.   
   
**Delta Aggregation** (n): An aggregation that occurs that only loads data into IdentityNow that has changed, been added, or been removed. Only some sources support this.   
   
**Deprovisioning** (n): The process of removing user access to systems, applications, and databases. Occurs automatically in all orgs that use provisioning. Also used in some certification configurations to automatically remove access that was revoked.   
   
**Directory Password** (n): An access management type that allows users to authenticate with credentials that are managed by and used for a source.   
   
**DN** (n): Distinguished Name.   
   
## E   
   
**Entitlement** (n): A set of specific permissions granted within a computer system, such as access to a particular building (based on a user's key badge), access to files and folders, or access to certain parts of websites. Entitlements also define the actions a user can take against the items they have access to.   
   
**Exclusion Rule** (n): A snippet of code that defines a filter for the contents of a certification campaign.   
   
## F   
   
**Federation** (n): A single sign-on method involving an authentication ticket or token, which is trusted across multiple systems or organizations.   
   
## G   
   
**Generator** (n): A snippet of code that creates the appropriate value for an identity attribute based on information you can configure.   
   
**Governance Group** (n): A group of people who can govern access to apps and data. For example, a governance group can be used to review an access request.   
   
## H   
   
**Helpdesk Administrator** (n): A person responsible for assisting users with basic IdentityNow access. They can enable, disable, and unlock accounts. They can view activity and interact with identity data but they cannot make changes to sources, apps, and many other features within IdentityNow.   
   
**Home** (n): The first page users see when they sign in. This page contains the User Dashboard.   
   
## I   
   
**Identity** (n): An authoritative account that includes first name, last name, and email. This account can own other accounts, entitlements, and attributes.   
   
**Identity Cube** (n): All of the information associated with an identity, including all of their accounts on all sources, all attributes and entitlements of those accounts, as well as IdentityNow attributes and entitlements such as the lifecycle state and SailPoint status. This is all the data associated with an identity within the IdentityNow product.   
   
**Identity Exception** (n): This identity is missing mandatory key data such as e-mail address or family name, making it invalid.   
   
**Identity Outlier** (n): A peer group of only one identity. The entitlements associated with the identity are too unique to include the identity in a peer group.   
   
**Identity Profile** (n): Instructions for creating and managing identities from the associated authoritative source or sources. These instructions determine a variety of security settings specific to the population managed in the source; the source of the attributes for that population; and, when Provisioning is enabled on the org, how access is granted for those identities when their lifecycle state changes or new identities are added from the source.   
   
**Identity Provider** (n): The entity in a federated relationship that declares to the service provider, or app, that a user is valid and has permission to authenticate into the app. The identity provider sends the service provider the authentication token used to grant access to the user.   
   
**IdentityNow Service** (n): A distinct set of functionality within IdentityNow, focused on solving a particular business problem. For example, Access Request, Password Management, Provisioning.   
   
**Integration** (n): A way that IdentityNow interacts with another product, to make use of features or data from that product from within IdentityNow.   
   
**IQService** (n): A service native to Windows that allows IdentityNow to access information and operate in a Windows environment. This service is necessary for IdentityNow to communicate with many sources.   
   
**IT Administrator** (n): Within IdentityNow, another term for Administrator.   
   
**IT Role** (n): In IdentityIQ, IT Roles encapsulate sets of system entitlements that are tied to actual permissions within an application or target system. They represent the actual state of the user’s access, such as an account, entitlement, or permission. A user’s IT roles can be detected in IdentityIQ based on the entitlements that user has. Access can also be provisioned in IdentityIQ through IT roles.   
   
## J   
   
**Joiner-Mover-Leaver** (n): Sometimes abbreviated JML. Three different types of provisioning supported by IdentityNow. Joiner refers to the action taken when an identity joins an organization. Mover refers to the actions taken to change their access if they move departments. Leaver refers to the actions that revoke access from the identity when they leave the company for any reason.   
   
## K   
   
**Knowledge-Based Authentication** (n): Often called KBA. A form of strong authentication that requires the user to have knowledge unique to the identity they're trying to sign in as. For example, security questions require a user to have prior knowledge to authenticate.   
   
## L   
   
**Lifecycle State** (n): A term for the employment stage an employee at a company is in. For example, users might be "Pre-Hire," "Employee," or "On Leave."   
   
**Limited Availability** (n): Indicates a new set of functionality that an IdentityNow customer can request access to in advance of the planned release to production. A customer's ability to participate might depend on a number of factors. The related Product Manager makes the final decision about participants. Users should be aware of the feature's limitations and work with their SailPoint contact to make suggestions or request assistance.   
   
## N   
   
**Nightly Refresh** (n): Synonym for Periodic Consolidated Refresh.   
   
**Non-Employee** (n): Any contractor, intern, consultant, or other user in your organization who isn't a full-time permanent employee.   
   
## O   
   
**Org** (n): Short for Organization.   
   
**Organization** (n): A company's IdentityNow system, configurations, users, apps, and everything else managed within IdentityNow.   
   
## P   
   
**Password Interceptor** (n): A feature of IdentityNow that, when installed and configured, can detect password changes on some sources and propagate them to other sources and apps.   
   
**Peer Group** (n): A grouping of identities, generated by machine learning, that have similar entitlements.   
   
**Periodic Consolidated Refresh** (n): A refresh job that is performed at 8am and 8pm CDT every day to ensure that all related data is synced based on changes that occurred during the previous 12 hours. In the System Activity page, this appears in the Type column as Identity Refresh or Role Refresh.   
   
**Potential Role** (n): A bundle of access that Role Discovery suggests as a role based on machine learning and user access patterns.   
   
**Private App** (n): An app for which the account credentials are not owned or monitored by your IT department.   
   
**Privileged** (adj): Describes an entitlement, access profile, or role that is particularly sensitive or important. Admins can set the Privileged badge for an entitlement to draw attention to it when a manager is doing certifications. Access profiles that contain this entitlement will also be marked as privileged, as will roles that contain those access profiles.   
   
**Provision** (v): To move data from within IdentityNow to any source. Also to make changes to any data, user, or permissions on a source from within IdentityNow.   
   
**Provisioning** (n): The process or granting, changing, or removing user access to systems, applications, and databases based on the related identity profile and the configuration instructions defined for the related source.   
   
## R   
   
**Recommendation Engine** (n): A SailPoint AI service that uses peer group analysis and identity attributes to recommend access to users and help certifiers decided whether access requests should be approved or denied. Includes Access Request Recommendations and Certification and Approval Recommendations.   
   
**Redirect Patterns** (n): URLs or URL patterns you have configured as approved, safe websites your users can be redirected to when they sign out of an app. This is only available when using certain configurations.   
   
**Refresh** (n/v): (n) After a change to configuration data related to identities, the act of making the data changes in the IdentityNow database where it can be used by admins. (v) To account for the data related to a refresh across applicable parts of the IdentityNow database so that it can be used by admins.   
   
**Relying Party** (n): A Service Provider. This term is commonly used in WS-Federation.   
   
**Request Center** (n): The page containing the list of all available apps a user can request access to. Approved applications can be found in the My Access and My Team tiles on their home page.   
   
**Report Admin User** (n): A type of user in IdentityNow that has permissions to view and download reports from the Search, Certifications, Access History, and Data Explore interfaces.   
   
**Role** (n): A label given to a group of users, based on their meeting certain criteria, that grants them access to specific apps and sources.   
   
**Role Admin User** (n): A type of user in IdentityNow that has permissions to view and manage roles, as well as use Search.   
   
**Role Discovery** (n): Included with the Access Modeling service. Uses machine learning to identify user access patterns and determine potential roles, or bundles of access. New roles can be automatically created from a potential role.   
   
**Role Insights** (n): Included with the Access Modeling service. Provides a greater understanding of an organization's role program, and suggests changes to existing roles to make them more secure.   
   
**Role Sub-Admin User** (n): A type of user in IdentityNow that has permissions to view, create, and manage roles with access profiles on sources that are associated with the governance groups they are members of. Sub-admins have the ability to search all organization data, not just data associated with their governance group.   
   
## S   
   
**SAML** (n): Security Assertion Markup Language (SAML) is an XML standard that allows secure web domains to exchange user authentication and authorization data. Using SAML, an online service provider can contact a separate online identity provider to authenticate users who are trying access secure content.   
   
**Secure Tunnel** (adj): Also known as the virtual appliance proxy tunnel or single point of access, this is a configuration for the virtual appliance that defines a very limited set of outbound connections generated by the virtual appliance (VA).   
   
**Separation of Duties** (SoD) (n): A service of IdentityNow that helps admins maintain control of the checks and balances of access that keep an organization safe.   
   
**Service Account** (n): The administrative account or any account on any system that manages that system.   
   
**Service Integration Module** (SIM) (n): An integration between IdentityNow's provisioning service and a 3rd party application that causes provisioning activity in IdentityNow to generate a related asset in the 3rd party service application. Currently, ServiceNow is the only supported application.   
   
**Service Provider** (n): The entity in a federated relationship that a user authenticates into. Usually an app or another site.   
   
**Sign In** (v): To gain access to a system by authenticating into the system either by entering identifying credentials or using another supported method.   
   
**Single Sign-On** (n): A feature of IdentityNow (and other access management software) that allows a user to sign in to one system that gives them access to several other systems at the same time. For example, a user can sign in to IdentityNow and, without entering more passwords, also use Box and other apps.   
   
**Source** (n): (1) A third party application, database, or directory management system that maintains its own set of users. IdentityNow collects data from these sources, including user information. (2) A representation of that source within the IdentityNow user interface you use to work with those accounts.   
   
**Source Admin User** (n): A type of user in IdentityNow that has permissions to view and manage sources, as well as use Search.   
   
**Source Sub-Admin User** (n): A type of user in IdentityNow that has permissions to view, create, and manage sources and access profiles only on the sources associated with the governance groups they are members of. Sub-admins have the ability to search all organization data, not just data associated with their governance group.   
   
**SSL** (n): Stands for Secure Socket Layer. SSL is a connection between two computers that encrypts everything sent over the connection.   
   
**Step-Up Authentication** (n): Another term for Strong Authentication.   
   
**Strong Auth** (n): Short for Strong Authentication.   
   
**Strong Authentication** (n): Within IdentityNow, a feature that allows users to verify their identity through a method other than a password. This can be done by retyping a password or using several other verification methods. This is used to ensure that the user is who they say they are before accessing particularly sensitive information.   
   
**Synchronize Attributes** (v): An action an administrator can take on an individual identity's account to copy certain identity attributes' values from the identity record to the related account on the source. This option is only available for accounts on sources that have at least one attribute selected in the Attribute Sync page of the source's configuration. Selecting this action manually updates the attributes for the associated identity. However, the system synchronizes all accounts on configured sources every 12 hours.   
   
## T   
   
**Task Manager** (n): A list of all the provisioning tasks assigned to and completed by the signed in user.   
   
**TLS** (n): Stands for Transport Layer Security. TLS is a more updated and secure version of SSL (Secure Socket Layer), and is a connection between two computers that encrypts everything sent over the connection. SSL and TLS are sometimes used interchangeably. However, IdentityNow supports TLS encryption.   
   
## U   
   
**Uncorrelated** (adj): If data has been aggregated but is not associated with any existing identities, it is considered uncorrelated.   
   
**User** (n): A person who accesses the IdentityNow system, or any other computer system.   
   
**User Dashboard** (n): On the Home page of IdentityNow, the page that displays the widgets available to users to track their work, access, and team.   
   
**User Managed** (n): An access management type that allows the credentials for an app to be controlled by the user, even when the apps are assigned by IT.   
   
**User Name** (n): The set of characters that identifies and represents a user within a computer system, and is often used to gain access to that system.   
   
## V   
   
**VA** (n): Short for Virtual Appliance.   
   
**Virtual Appliance** (n): A virtual machine (VM) running behind your organization's firewall to support certain types of single sign-on to applications that also reside behind the firewall. In most cases, the virtual appliance encrypts your users' authentication data before sending it to IdentityNow so that systems and account data behind your firewall are not exposed.   
   
## W   
   
**WS-Federation** (n): An abbreviation for "Web Services Federation." WS-Federation is a type of authentication protocol that allows users to authenticate into an app without using a password.