---
category: '2022'
created: 2022-11-03 23:31:31.469000+00:00
id: d06959dd-d826-4944-9e72-fc54e2339d6a
tags:
- meta
- '553'
title: Git Commit Current File
updated: 2022-11-03 23:31:31.789000+00:00
---
   
Sometimes I'm too lazy to open the vault in the terminal and do a commit for a single file, so I've made this very simple template that will commit the current file with a custom commit message.   
   
```
<%* 
tp.user.git_add({file: tp.file.path()}) 
const msg = await tp.system.prompt("Commit message", "", true)
if (msg != "") {
  tp.user.git_commit({message: msg})
}
-%>
```
   
   
It's nothing special as you can see, but quite handy at times, and also shows how one can use arguments with 'system command functions'   
   
I've left the `git add` outside of the if condition as it makes things a bit more flexible, e.g committing several files, but in this case I'll probably not use the template.   
   
Requires two User System Command Functions:   
   
   
-   `git_add`: `git add "$file"`   
-   `git_commit`: `git commit -m "$message"`   
   
via — [git commit current file · Discussion `{_obsidian_pattern_tag_553}` · SilentVoid13/Templater · GitHub](https://github.com/SilentVoid13/Templater/discussions/553)