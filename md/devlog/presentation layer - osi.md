---
created: 20211010130635116
desc: ''
id: 2nnii3yd2gbdvevk0zxu9m1
title: Presentation Layer - OSI
updated: 1656561830210
---
   
# Layer 6 – Presentation Layer   
   
   
- Responsible for formatting the data exchanged and securing the data with proper encryption.   
- Functions:   
  - Data formatting   
  - Encryption   
   
As suggested by the name itself, the presentation layer will present the data to its end users in the form in which it can easily be understood. Hence, this layer takes care of the syntax, as the mode of communication used by the sender and receiver may be different.   
   
### Data Formatting   
   
   
- Formats data for proper compatibility between devices.   
  - ASCII   
  - GIF   
  - JPG   
- Ensures data is readable by receiving system   
- Provides proper data structures   
- Negotiates data transfer syntax for the [Application Layer - OSI](../devlog/application%20layer%20-%20osi.md)   
   
   
---   
   
### Encryption   
   
   
- Used to scramble the data in transit to keep it secure for prying eyes.   
- Provides confidentiality of data.   
- E.g.   
  - [TLS](../devlog/tls.md) to secure data between your PC and website.   
   
   
---   
   
### Layer 6 Examples   
   
**Presentation styles** - taking ones and zeros and present them in the human readable format?   
   
   
- [HTML](/not_created.md), [XML](/not_created.md), [PHP](/not_created.md), [languages.javascript](../devlog/languages.javascript.md)   
- [ASCII](/not_created.md), [EBCDIC](/not_created.md), [UNICODE](/not_created.md)   
- GIF, JPG, TIF, SVG, PNG   
- MPG, MOV   
   
**Encryption styles** - how do we secure data in a jumbled format?   
   
   
- [TLS](../devlog/tls.md), [SSL](../devlog/ssl.md)