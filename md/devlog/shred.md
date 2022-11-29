---
created: 20211022112521504
desc: ''
id: nopt07i3l3suxtq0xh5mg6h
title: shred
updated: 1652815514811
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`shred` is a program that will overwrite your files in a way that makes them very difficult to recover by a third party.   
   
Normally, when you delete a file, that portion of the disk is marked as being ready for another file to be written to it, but the data is still there. If a third party were to gain physical access to your disk, they could, using advanced techniques, access the data you thought you had deleted.   
   
The analogy is that of a paper shredder. If you crumple up a piece of paper and throw it in the trash can, a third party could come along, root through your trash, and find your discarded documents. If you want to destroy the document, it's best to use a paper shredder. Or burn it, I suppose, but that's not always practical in a typical office.   
   
The way that shred accomplishes this type of destruction digitally is to overwrite (over and over, repeatedly, as many times as you specify) the data you want to destroy, replacing it with other (usually random) data. Doing this magnetically destroys the data on the disk and makes it highly improbable that it can ever be recovered.   
   
> —via [Linux shred command help and examples](https://www.computerhope.com/unix/shred.htm)   
   
Example:   
   
   
- `cp /etc/passwd .` to copy an important file to current working dir   
- `shred -vu -n 100 passwd` where `-v` verbose `-u` removing after overwriting `-n 100` overwrites data 100 times instead of 3(which is the default)