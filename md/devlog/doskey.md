---
created: '2022-04-10T00:00:00.000Z'
desc: ''
id: 7c3uvxcktatvsjsibu3bhaq
title: Doskey
updated: 1652622336394
---
   
Topics::  [Windows](../devlog/windows.md)   
   
   
---   
   
the DOSKEY command can be used to define macros, which are analogous to aliases.   
   
```
doskey macroName=macroDefinition
```
   
   
Macro parameters are referenced in the definition via `$` prefixed positions: `$1` through `$9` and `$*` for all.   
   
See the [doskey technet documentation](https://technet.microsoft.com/en-us/library/bb490894.aspx), or type `doskey /?` or `help doskey` from the command line for more information.   
   
But there are serious limitations with DOSKEY macros:   
   
   
- The macros only work on the interactive command line - they do not work within a batch script.   
- They cannot be used on either side of a pipe: Both `someMacro|findstr '^'` and `dir|someMacro` fail.   
- They cannot be used within a FOR /F commands: `for /f %A in ('someMacro') do ...` fails   
   
The limitations are so severe that I rarely use DOSKEY macros.   
   
Obviously you can create batch scripts instead of macros, and make sure the script locations are in your PATH. But then you must prefix each script with CALL if you want to use the script within another script.   
   
You could create simple variable "macros" for long and oft used commands, but syntax is a bit awkward to type, since you need to expand the "macro" when you want to use it.   
   
Definition:   
   
```
set "cdMe=cd a_very_long_path"
```
   
   
Usage (from command line or script)   
   
```
%cdMe%
```
