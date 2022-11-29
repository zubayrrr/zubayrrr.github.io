---
created: 20211130161918584
desc: ''
id: bq0gblqc282v024og4l0v5c
title: Data Mart
updated: 1653318643707
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
Dependent and Independent(of [data warehouse](../devlog/data%20warehouse.md)) data marts.   
   
### Dependent   
   
   
- Sources from Data Warehouse   
- (Mostly) uniform data across marts   
- Architecturally straightforward   
- Many sources   
- ETL from sources   
- Probably large data volumes   
- Dimensionally organized data   
   
### Independent   
   
   
- Sourced directly from applications and systems   
- Little or no uniformity across marts   
- "Spaghetti" architecture   
- One or more sources   
- ETL from sources   
- Possibly large data volumes   
- Dimensionally organized data