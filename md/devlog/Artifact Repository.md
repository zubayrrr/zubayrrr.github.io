---
created: 1654593468630
desc: ''
id: slohd4hnb6y31jj538tm0do
title: Artifact Repository
updated: 1654593468630
---
   
## Artifacts   
   
   
- Artifacts are apps built into a single, shareable, portable file.   
- Building Java applications produce a special artifact file such as a `.jar` or a `.war`.   
- Apps built from other programming languages may result in different artifact files such as a zip or a tarball.   
   
See also: [Artifact Repository](../devlog/Artifact%20Repository.md)   
   
   
   
Artifact repository is nothing but a place to store artifacts. The artifact repository has to support the artifact format. There are different artifact repositories formats for different artifact types/formats.   
   
If you're dealing with different types of artifacts, you need different artifact repositories. Which is Artifacts Repository Managers come into the picture.   
   
## Artifact Repository Manager   
   
Artifact Repository Manager is a piece of software lets you manage all your different artifacts repository formats in a centralized way. It provides one end-point and one interface to access all your types artifact repositories.   
   
One of the most popular Artifact Repository Manager is [nexus](../devlog/nexus.md) (private or internal use only).   
   
There are public repository managers as well such as [mvnrepository.com](https://mvnrepository.com), [npmjs.com](https://www.npmjs.com/) that host publicly available libraries, frameworks that are used as dependencies.