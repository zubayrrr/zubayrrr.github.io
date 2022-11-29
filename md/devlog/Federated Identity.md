---
aliases:
- Federated Identity
- Federated Identity
category: '2022'
created: 1666042654788
desc: ''
id: a7b5642e-2198-4f03-9b2c-9045e4939541
title: Federated Identity
updated: 1666042654788
---
   
Related::  [idP](../devlog/idP.md)   
   
---   
   
It is basically two Identity Providers talking to and trusting each other.   
   
Identity federation is the process where the authentication responsibility of a user is delegated to an external partner.   
   
Think of it as two partners: one of them (Federated Identity Provider) provides the identity of the user, the other provides only the service or application the user is trying to access. The second partner (let’s call it Service Provider) delegates the authentication responsibility to an external, trusted party - the Federated Identity Provider.   
   
This process is called federation, where the Federated Identity Provider “vouches” for the identity of the user, the Service Provider trusts the IdP, and allows the user to access whatever the service or application is.   
   
## **Federated Identity Management vs. SSO**   
   
Federated Identity Management (FIM) and Single Sign-On (SSO) are closely related, but they are not the same. There is a clear distinction between them and **they are in no way synonymous**.   
   
Yes, Single Sign-On, as the name suggests, allows a user to sign in to multiple services or applications with a single login. However, Federated Identity Management reaches much further. While SSO gives you access to applications or systems within an organisation, with FIM you can access applications or systems across several different enterprises. It is a broader concept where two identity management systems are connected and work together seamlessly, based on mutual trust. As a result, Federated Identity Management systems can give you SSO, but it doesn't necessarily work the other way around.   
   
For example, anytime you use your Facebook account to access a service such as Airbnb, you're seeing identity federation in action. This is because Facebook and Airbnb are completely separate systems, but with a Federated Identity Management system you can use one to access the other. However, when you use your Google account to access Gmail and Google Maps you're still within the same "organisation", meaning you're using SSO. But if you were to use that Google account to access Quora message boards, then it would be FIM again. For the user, the distinction can become blurry in practice, which is a sign that the user experience is smooth.   
   
## **Identity Federation and SAML SSO?**   
   
We are increasingly seeing federation being referred to as “SAML SSO”. If a company says that it supports SAML SSO what they likely mean is that they support identity federation. A user identity stored and authenticated in an Identity Provider that uses SAML 2 simply means that it is using the SAML 2 standard to authenticate and exchange user identity information with connected systems or applications for the purposes of Single Sign On.   
   
In more simple terms, a user (whose profile is stored in a SAML 2-based Identity Provider) can use her same login credentials to access multiple applications but only be required to login once, assuming that SAML SSO has been implemented for all connected applications. “SAML SSO” and “federated identity” in this case can be considered synonyms.   
   
[What is Identity Federation? | Guide to Federated Identity [2022]](https://www.10duke.com/blog/federated-identity/)