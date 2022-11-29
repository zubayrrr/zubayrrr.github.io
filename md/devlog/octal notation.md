---
created: 20211027095956416
desc: ''
id: jqnpryjto5mvfqztm2qtliw
title: Octal Notation
updated: 1653437412078
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- The number that represents the permissions in base-8 can be either a 3 or 4 digit number with digits from 0 to 7. The leading zero(0) can be omitted.   
- 0755 = 755 and 0644 = 644   
- When a 3 digit number is used, the first digit represents the permissions of the file's owner, the second one the file's group, the last one the permissions of the other class.   
- `r`, `w` and `x` have their own fixed number value:   
  - `r` read = 4   
  - `w` write = 2   
  - `x` execute = 1   
  - `-` no permissions = 0   
  - The permissions number of a specific user class is represented by the sum of the values of the permissions of that group.   
- Examples:   
  - `rwx` = 4 + 2 + 1 = 7   
  - `rw-` = 4 + 2 + 0 = 6   
  - `r--` = 4 + 0 + 0 = 4   
- Examples with all permissions:   
  - `rw-rw-r--` = `4 + 2 + 0`, `4 + 2 + 0`, `4 + 0 + 0` = 664   
  - `rwxr---wx` = `4 + 2 + 1`, `4 + 0 + 0`, `0 + 2 + 1` = 743   
  - `rwxr-xr` = 754   
- Use [stat](../archive/STAT.md) to verify ocatal notation with symbolic one (`ls -l`)