---
created: 20211130161032384
desc: ''
id: oppcapyr6oew027thjm2z91
title: Data Warehouse Architecture
updated: 1653318643711
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
### Centralized [data warehouse](../devlog/data%20warehouse.md)   
   
   
- A single data warehousing environment, rather than one made up of multiple components.   
- Ideally, it should be your default or "go to" architecture   
- Single Database   
- Obvious advantage: One stop shopping(of data)   
- High cross-org cooperation   
- High data governance   
- Ripple effects   
- Emphasis on "enterprise" (EDW)   
  - Relational   
  - Specialized Database (DWing appliances)   
   
### Component Based   
   
   
- Decomposition   
- Mix and match technology   
- "Bolt together" components   
- Overcome org. challenges   
- Often inconsistent data   
- Difficult to cross-integrate   
  - Architected would contain   
  - DW + DMs   
- Or simply DMs only   
- DW Bus all DMs follow "Conformed Dimensions"   
- Non-Architected   
  - Federated EDW   
   
See also: [Data Mart]([data mart](../devlog/data%20mart.md))