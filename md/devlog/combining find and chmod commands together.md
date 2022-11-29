---
created: 20211027125030936
desc: ''
id: 8f7fkugnclgo7744xnma2d2
title: Combining Find and Chmod Commands Together
updated: 1653683867190
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
To recursively set permissions for all files to a specific value, you should exclude the directories in the path otherwise the directories will have same permissions as the files, see: [The Effect of Permissions on Directories](../devlog/the%20effect%20of%20permissions%20on%20directories.md)   
   
To mitigate this, we can combine [find](../devlog/find.md) and [chmod](../devlog/chmod.md) commands together   
   
Example   
   
   
- `find ~ -type f -exec chmod 640 {} \;` for all files   
- `find ~ -type d -exec chmod 750 {} \;` for all directories