---
created: '2022-05-12T00:00:00.000Z'
desc: ''
id: z47uqjeaxrmr0ujjuiwul7t
title: PPA
updated: 1652815757505
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
PPA stands for Personal Package Archive. The PPA allows application developers and Linux users to create their own repositories to distribute software. With PPA, you can easily get newer software version or software that are not available via the official Ubuntu repositories.   
   
Mind the word ‘Personal’ here. That gives the hint that this is something exclusive to a developer and is not officially endorsed by the distribution.   
   
## Why PPA? Why not DEB packages?   
   
You may ask why should you use PPA when it involves using command line which might not be preferred by everyone. Why not just distribute a DEB package that can be installed graphically?   
   
The answer lies in the update procedure. If you install a software using a DEB package, there is no guarantee that the installed software will be updated to a newer version when you run sudo apt update && sudo apt upgrade.   
   
It’s because the apt upgrade procedure relies on the sources.list. If there is no entry for a software, it doesn’t get the update via the standard software updater.   
   
So does it mean software installed using DEB never gets an update? No, not really. It depends on how the package was created.   
   
Some developers automatically add an entry to the sources.list and then it is updated like a regular software. Google Chrome is one such example.   
   
Some software would notify you of availability of a new version when you try to run it. You’ll have to download the new DEB package and run it again to update the current software to a newer version. Oracle Virtual Box is an example in this case.   
   
For the rest of the DEB packages, you’ll have to manually look for an update and this is not convenient, especially if your software is meant for beta testers. You need to add more updates frequently. This is where PPA come to the rescue.   
   
> via — [What is PPA? Everything You Need to Know About PPA in Linux](https://itsfoss.com/ppa-guide/)