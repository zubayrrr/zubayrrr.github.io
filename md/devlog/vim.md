---
created: '2021-10-23T00:00:00.000Z'
desc: ''
id: guawfkvsbkg1eo8o36sdqxh
title: vim
updated: 1653437919626
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- `vim` is a text editor that is upwards compatible to `vi`. Infact in most distros, vi is [Aliases](../devlog/aliases.md) to vim. It stands for "Vi Improved".   
   
There are a lot of enhancements above vi: multi level undo, multiple windows and buffers, syntax highlighting, command line editing, file name completion, a complete help system, visual selection, and others.   
   
### `vim` is a modal editor, it has two primary "modes":   
   
COMMAND mode and INSERT mode.   
   
In COMMAND mode, you execute commands (like undo, redo, find and replace, quit, etc.). In INSERT mode, you type text. There is a third mode, VISUAL mode, that is used to highlight and edit text in bulk.   
   
   
- To go into INSERT mode from COMMAND mode, you type `i`.   
- To go back to COMMAND mode, you type the `esc` key.   
   
   
---   
   
   
- <span class="underline">vim starts out in COMMAND mode</span>.   
- <span class="underline">Note that all commands mentioned below (except for arrow keys) only work in COMMAND mode.</span>   
   
### Entering INSERT Mode   
   
When you are ready to enter text, you should switch to INSERT mode. There are a few ways to do this:   
   
   
- `i` enter INSERT mode before the cursor   
- `I` enter INSERT mode at the start of the current line   
- `a` enter INSERT mode appending after the cursor   
- `A` enter INSERT mode appending to the end of the current line   
- `o` enter INSERT mode on a new line below the current line   
- `O` enter INSERT mode on a new line above the current line   
   
Then, just type as normal to enter text. You can use the arrow keys to navigate, or switch back to COMMAND mode.   
   
### Last Line Mode   
   
You can enter the Last Line Mode from the COMMAND mode((`esc`) using `:` colon key, after pressing the colon, you can do all sorts of things from this mode.   
   
### Highlighting text   
   
If you want to highlight multiple lines or particular words in a line, you can do so in VISUAL mode. There are three different visual modes:   
   
   
- `v` enters character-wise visual mode to highlight one character at a time.   
- `V` enters line-wise visual mode to highlight entire lines at a time.   
- `ctrl-v` enters block-wise visual mode to highlight over rows and columns, etc.   
   
Once you enter these modes by typing these in COMMAND mode, you can use the keyboard navigation (e.g., `hjkl` or `w` or `b`) to highlight text). Then you can batch delete (`d`), yank (`y`), or paste (`p`) whatever is highlighted. To exit VISUAL mode, use `esc`.   
   
VISUAL mode is also useful for adjusting indent to a batch of text. For example, if you wanted to reduce the indent of a set of lines, you can enter block-wise visual mode (`ctrl-v`) to select a vertical column of indents (using keyboard navigation), and then batch delete with `d`. To increase the indent of a set of lines, enter block-wise visual mode and select a vertical column, and then batch insert at the beginning of this block with `I`, type in your indentation, and then use `esc`. You should see all highlighted lines get the same inserted space.   
   
### Examples   
   
   
- `ZZ` shift zz to save and quit quickly.   
- `gg` to move to the start of the file.   
- `/` followed by the string and press enter to forward search,     
  `n` to find the next occurrence and `N` to search in opposite direction, just like [less](../devlog/less.md)   
   
- `G` or `Shift + g` to move you to the bottom of the file.   
- `?` followed by the string and press enter to backward search.   
- Press `*` to find the next occurance of the word under the cursor.   
- Press `#` to find the previous occurance of the word under the cursor.   
   
   
---   
   
   
- `u` undo the last action   
- `U` undo all recent changes made to the current line   
- `ctrl-r` redo   
- `:e!` undo till the last saved version of the file   
   
   
---   
   
   
- `:w myprogram.c` save the current changes to a file. If you don't specify a name, changes will be saved to the current file. If you would like to save the file under a different name, specify a filename.   
- `:q` quits Vim. If you have unsaved changes, you will be asked whether or not you'd like to save your changes before quitting.   
- `:q!` quit without saving unsaved changes.   
- `:wq` save and quit.   
- `:!` to run the shell commands like `:!dir`, `:!ls`   
- `:` followed by the line number to move to that specific line   
- `:%s/foo/bar/g` Subsitute all matches of the word `foo` in the file with `bar`. where `g` stands for globally. To ignore case in search use `gi`   
- `:set nu` to give line numbers, `:set nonu` to remove line numbers   
- `:syntax on` to turn on syntax highlightings and `:syntax off` to turn off   
   
   
---   
   
   
- `dd` to cut a line (copied to the clipboard)   
- `Shift + p` to paste before the cursor   
- `p` to paste after the cursor   
- To cut more than one line from the cursor, type the number of lines and `dd`   
- `v` to start selectng, navigate with arrow keys to define the selection   
- `Shift + V` to select the entire line   
- `Ctrl + V` to select in rectagular boxes   
- `y` yank to copy   
   
   
---   
   
   
- Create a file `.vimrc` in the user's home dir and write all the commands you'd write in the last line mode that you'd like to be <span class="underline">persistent</span>.   
- Open multiple files in `vim file1 file2`   
  - `:n` or `:next` to go to the next file   
  - `:N` or `:prev` to go the previous file   
- To open multiple files in stacked mode `vim -o file1 file2`   
  - `Ctrl + w` to switch between files   
- To open files side by side (split) that shows [diff](../devlog/diff.md) `vim -d file1 file2`   
  - You can also use `vimdiff` the wrapper to show the [diff](../devlog/diff.md) between two files   
  - `Ctrl + w` to switch between files   
- When `vim` is closed unconventionally, the next time you open the same file with vim, you'll be prompted about a swap file for the file you previously worked on, you can recover the file by pressing `R` and saving it or simply delete the file that was created. `rm .fileName.swp` and you'll be able to open it normally.   
   
> —via [CS107 The Vim Editor](https://web.stanford.edu/class/archive/cs/cs107/cs107.1218/resources/vim.html)