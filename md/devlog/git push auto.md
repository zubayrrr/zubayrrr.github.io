---
category: '2022'
created: 2022-07-13 16:18:27.633000+00:00
id: git push auto
tags:
- devlog
- tidbits
title: JI - 1546948817462800384
updated: 2022-11-05 10:52:40.225000+00:00
---
   
Related:: [version control.git](../devlog/version%20control.git.md)   
   
   
---   
   
With the newest version of Git 2.37.0, you can run just "git push" to push new branches. No more "--set-upstream origin". Enable with:   
   
`git config --global --add --bool push.autoSetupRemote true`\   
   
via — [https://twitter.com/JI/status/1546948817462800384](https://twitter.com/JI/status/1546948817462800384)