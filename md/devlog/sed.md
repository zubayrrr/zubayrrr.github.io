---
created: 20211123201031068
desc: ''
id: 0dlw6puljva6zl22z1uai4x
title: sed
updated: 1652815757462
---
   
   
- `topics:` [linux](../topics/linux.md)   
- `resources:` [The Grymoire's tutorial on SED](/not_created.md)   
   
   
---   
   
`sed` command is used for string replacement   
   
### Example   
   
If we want to eliminate the "," in "Kutuzov," and redirect the output to a new-file   
   
`sed 's/Kutuzov,/Kutuzov/' war-and-peace.txt > new-file`