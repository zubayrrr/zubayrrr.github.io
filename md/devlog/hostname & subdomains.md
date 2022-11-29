---
created: 1656340839760
desc: ''
id: tuw0j4c7vfenoapeh8816kj
title: Hostname & Subdomains
updated: 1656341728277
---
   
Topics::  [networking](../topics/networking.md)   
   
   
---   
   
The hostname is what a device is called on a network. Alternative terms for this are computer name and site name. The hostname is used to distinguish devices within a local network. In addition, computers can be found by others through the hostname, which enables data exchange within a network, for example. Hostnames are used on the internet as part of the fully qualified domain name.   
   
Differentiation between hostname, domain and fully qualified domain name   
   
The hostname is a freely selectable name for a host. For example, you could call a server in a company network responsible for the central administration of emails “mail” or “mail123”.   
   
However, if a computer needs to be available over the internet as well as locally, the hostname needs to be supplemented by information that indicates what part of the internet the computer is located in. In the internet, computers can be uniquely assigned using a combination of hostname and domain. These uniquely identifiable name chains are known as a “Fully Qualified Domain Name“ (FQDN). An example of an FQDN would be:   
   
mail123.example.com.   
   
If you read the terms of the hierarchy from right to left, you can recognize the components of the FQDN in the following order: root label (empty), top level domain (.com), second level domain (example) and hostname (mail123).   
   
An FQDN is a human-readable form of addressing. Unlike humans, computers work with numerical IP addresses to uniquely identify computers on the internet. Within the framework of a website visit, an intermediate step is necessary so that the alphanumeric domain can be translated into a numeric IP address.   
   
The domain name system (DNS) is responsible for this name resolution. The entered domain is assigned to the corresponding IP address and then the searched-for page is called up. The purpose of this system is so that humans do not have to enter the IP address every time they visit a website, but can use a name that will be easier to remember instead.   
   
Do not confuse the hostname with a subdomain. This is also located to the left of the top-level domain, but does not designate a computer or server, just the domain area. The hostname is still far on the left. Example: In the FQDN www.example.ionos.com, “IONOS” denotes a domain name, “example” denotes a subdomain and www is the hostname.   
   
— via [What is a Hostname? Meaning, Example & how to check - IONOS](https://www.ionos.com/digitalguide/hosting/technical-matters/hostname/)   
   
## Hostname vs Subdomain   
   
Basically, "domain" and "subdomain" are the same entities, except that the "sub" prefix indicates a relationship between two domains. So you can basically talk of a "subdomain" only in relationship to another domain. For example `google.com` and `corp.google.com` both are domains, but `corp.google.com` is a subdomain of `google.com`. `google.com` itself is also a subdomain, a subdomain of top level domain (TLD) `com`.   
   
TLDs are the only domains that you can't talk of as "subdomains", because they don't have any higher-level domain above them.   
   
It's similar to how a file system on a computer is organized: `/usr` and `/usr/bin` are both folders, but `/usr/bin` is a subfolder of `/usr`. `/usr` is a subfolder of the root folder (`/`). The root folder is the only folder that isn't a subfolder of anything.   
   
Technically, any domain should have one or more **NS records** in the DNS, specifying the name server(s) serving that domain. It is possible to define a domain without it's own NS record, but this is considered trickery. One shouldn't set up DNS like that.   
   
Hostname - as said in the other answer - is just an individual name assigned to a computer. If you combine hostname with domain, you get a Fully Qualified Domain Name (FQDN), that identifies a particular computer in the DNS. Any FQDN should translate to an **A record** in the DNS, specifying the IP address assigned to that FQDN (or AAAA record in case of IPv6 addresses).   
   
One computer can have multiple hostnames and/or multiple FQDNs (even in different domains) which may be assigned either to the same IP address or to different IP addresses - this is fully flexible.   
   
For example, `ns1.google.com` is a FQDN of one of the Google's name servers. `ns1` is a hostname here (we sometimes call it a **hostname part of the FQDN**), and `google.com` is a domain (similarly, a **domain part of the FQDN**).   
   
Note that the domain name itself may also be considered a FQDN, especially when the domain itself is also assigned an A record, as it is common nowadays (see below).   
   
`www` is just a specific hostname that is customarily used to identify the main web server for the given domain. So `www.google.com` is FQDN of Google's main web server. It is common nowadays to configure DNS so that the domain itself also has A record that refers to the same IP address that the `www` hostname, so typing for example `https://google.com` and `https://www.google.com` brings you to the same website.   
   
Of course hostnames/FQDNs are not used only for webservers; any computer in the network can have a hostname/FQDN. For example, Gmail's incoming and outgoing mail servers have FQDNS `imap.gmail.com` and `smtp.gmail.com`. You don't type these FQDNs into the web browser, because there's no web service on these machines; but you use them eg. when configuring your mail client to use Gmail.   
   
— via [Difference between Subdomain, hostname, host and www in a DNS system? - Super User](https://superuser.com/questions/1644463/difference-between-subdomain-hostname-host-and-www-in-a-dns-system)   
   
## Resources   
   
   
- [Why Do Some Websites Start With WWW1? (Not WWW) - YouTube](https://www.youtube.com/watch?v=8Fq-hsGYS-8)