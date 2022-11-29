---
created: '2021-10-11T00:00:00.000Z'
desc: ''
id: 7si4f2a9dxq6li5izmp1lca
title: Man Pages
updated: 1652815757450
---
   
   
- `topic`: [linux](../topics/linux.md)   
   
   
---   
   
`man` command can be used to look for documentation on specific Linux commands.   
   
### Manual Structure   
   
<table>   
<thead>   
<tr class="header">   
<th>Section</th>   
<th>Contains</th>   
</tr>   
</thead>   
<tbody>   
<tr class="odd">   
<td>1</td>   
<td>User Commands</td>   
</tr>   
<tr class="even">   
<td>2</td>   
<td>System Calls</td>   
</tr>   
<tr class="odd">   
<td>3</td>   
<td>C Library Functions</td>   
</tr>   
<tr class="even">   
<td>4</td>   
<td>Devices and Special Files</td>   
</tr>   
<tr class="odd">   
<td>5</td>   
<td>File Formats and Conventions</td>   
</tr>   
<tr class="even">   
<td>6</td>   
<td>Games</td>   
</tr>   
<tr class="odd">   
<td>7</td>   
<td>Miscellaneous</td>   
</tr>   
<tr class="even">   
<td>8</td>   
<td>System Administration</td>   
</tr>   
</tbody>   
</table>   
   
   
---   
   
   
- Search the man pages for a specific by passing the option `-k` followed by search keyword, it'll return all the relevant man pages for the searched term.   
- Example: `man -k which` or `man -k "copy files"`   
- You can also use the command `apropos` to search just like `man -k`   
   
   
---   
   
   
- Search a specific section for a command.   
- Example: `man 1 which`   
   
   
---   
   
   
- When an option is inside square brackets it means that option is optional.   
- Example: `which [-a] filename ...`   
- `...` (Ellipsis) indicates that the command can take more than one input or options.   
   
   
---   
   
   
- Anything inside angle brackets is a mandatory argument to pass onto the command.   
- Example: `command <something>`   
   
   
---   
   
   
- Inside a Man Page **bold** text means you're supposed to type it exactly as described.   
- <span class="underline">Underlined</span> or _Italic_ text means you're supposed to substitute it with your requirement appropriately.   
- `Ctrl + F`, to move forward one window, `Ctrl + B`, to move backward one window, Arrow keys for going up or down.   
- `g` to go to the very beginning.   
- `G` to go to the very end.   
- To search for specific text inside a Man Page, press `/` and type the string you want to search for and hit enter.   
- Any matches found will be highlighted and you can use `n` to jump from matches and `Shift + n` to jump to previous match.   
- To search from the bottom of the Man Page (`G`) use `?` and type your string.   
- Press `q` to quit.   
   
   
---   
   
   
- If an option specifies a pipe symbol, the command would like you to pass either of the option, you cannot pass both.   
- Example: `command [-this | -that] ...`   
   
   
---   
   
   
- To view Man Pages in `less` mode press `h` key while you're on a Man Page.   
- [less](../devlog/less.md) command   
   
   
---   
   
   
- There are two type of commands, executables files on the disk and shell builtin commands.   
- To check if a command is an executable or a shell builtin command, use `type` followed by the command you want to check, example: `type df`, if it returns a path, its an executable and will have a dedicated [Man Page](../devlog/man%20pages.md)   
- If a command is a shell builtin, such as: `type cd`, it'll return "cd is a shell builtin".   
- `type` is also a shell builtin   
   
<!-- end list -->   
   
   
- To get help for shell builtin commands, use `help` command instead of `man`.   
- `--help` followed by a command, will return help pages for both executables and shell builtins.