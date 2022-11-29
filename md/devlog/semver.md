---
created: 1662342652242
desc: ''
id: wfae0w41a48mxo5zutjopm6
title: Semver
updated: 1662342745951
---
   
## What is Semver   
   
Semver is a specification outlining a method of encoding the nature of change between releases of a "public interface", directly into the version string.   
   
A public interface could be anything from an application programming interface (API), a command-line interface (CLI) or a graphical user interface (GUI). Anything that a third-party depends on having predictable interactions with should be versioned with semver. Semver could even be extended to physical interfaces, but we'll leave that as an exercise for your imagination.   
   
Semver is a scheme for interface versioning for the benefit of interface consumers, thus if a tool has multiple interfaces, e.g. an API and a CLI, these interfaces may evolve independent versioning. Although many applications do not consider their CLI to be part of their interface when versioning, a third-party may depend on specific CLI behaviour in the same way they might depend on an API.   
   
— via [Semver: A Primer - NodeSource](https://nodesource.com/blog/semver-a-primer/)   
   
   
---   
   
Given a version number MAJOR.MINOR.PATCH, increment the:   
   
   
- MAJOR version when you make incompatible API changes   
- MINOR version when you add functionality in a backwards compatible manner   
- PATCH version when you make backwards compatible bug fixes   
  Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.   
   
— via [Semantic Versioning 2.0.0 | Semantic Versioning](https://semver.org/)   
   
## Resources   
   
   
-