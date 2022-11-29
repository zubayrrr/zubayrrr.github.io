---
created: 1665626440952
desc: ''
id: a7htyjnczk581e9tvhvozqq
title: ServiceNow Okta Integration
updated: 1665626440952
---
   
**ServiceNow [Okta](../devlog/Okta.md) Integration**   
   
   
- Okta is a cloud-based identity management product which helps companies manage and secure user authentication and build identity controls into applications.   
- Single Sign-On ([SSO](../devlog/SSO.md)) using Okta as **Identity Provider** (IDP) and ServiceNow as **Service Provider** (SP) using [SAML](../devlog/SAML.md) authentication.   
   
**Auto user provisioning from Okta to ServiceNow**   
   
   
- Create Users: Creates or links a user in ServiceNow UD when assigning the app to a user in Okta   
- Update User Attributes: Okta updates a user’s attributes ServiceNow UD when the app is assigned. Future attributes changes made to Okta user profile will automatically overwrite the corresponding attribute value in ServiceNow UD.   
- Deactivate Users: Deactivate a user’s ServiceNow UD account when it is unassigned in Okta or their Okta account is deactivated. Accounts can be reactivated if the app is reassigned to a user in Okta.   
- Sync Passwords: Creates a ServiceNow UD password for each assigned user and pushes it to ServiceNow UD.   
- Password Type:   
  - Sync a randomly generated password.   
  - Sync Okta password.   
   
**Prerequisites for Implementation**   
   
   
- Administrative ServiceNow Account   
- Application Administrative Okta Account   
   
**Plugin for ServiceNow**   
   
   
- Login to ServiceNow as the System Administrator.   
- Search for “`com.snc.integration.sso.multi`” on the Plugins page.   
- Click install for the following plugins:   
  - **Multiple Provider Single Sign-On Enhanced UI**   
  - **Multiple Provider Single Sign-On Installer**   
   
**Set Properties in ServiceNow**   
   
   
- Search for “Multi-Provider SSO”, click on “Properties”.   
- Select “Yes” for Enable Multiple provider SSO and update “user_name” in the field for “User authentication login page”.   
   
**Okta Setup**   
   
   
- Login to Okta using admin privilege.   
- Go to “Applications” page from the left sidebar.   
- Browse app catalogue and search for ServiceNow UD application and click add.   
- Provide ServiceNow instance URL and configure Sign-On options.   
- Go to the ServiceNow UD application page on Okta and go to “Provisioning” tab and click “Configure API Integration”.   
- Provide ServiceNow Admin Username and Password and Test API Credentials.   
- Go back to “Provisioning” tab and click “edit” on **Provisioning to App** and enable **Create Users**, **Update User Attributes**, **Deactivate Users**, **Sync Password** (choose Sync Okta password as the password type) and save.   
- On **ServiceNow UD Attribute Mappings** section, click on “Go to Profile Editor” and verify the attributes.   
- From the ServiceNow UD application page, copy the metadata info link to be used when configuring ServiceNow.   
   
**ServiceNow Setup**   
   
   
- On **Identity Providers** page, click New to add a new identity provider.   
- Choose [SAML](../devlog/SAML.md) as SSO type.   
- Click on Name field to Import Identity Provider Metadata by entering the previously copied URL from Okta.   
- Make the necessary modifications in the tabs “User Provisioning” and “Advanced”.   
   
Detailed instructions can be found at: [Setup SSO](https://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-ServiceNow.html)   
   
## Resources   
   
   
- [ServiceNow Okta Integration - YouTube](https://www.youtube.com/watch?v=8uAh7Cyb59w)