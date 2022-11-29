---
created: 20211022103614668
desc: ''
id: 90j02txl52nf8d057um848y
title: rm
updated: 1652815757407
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The `rm` command is used to delete files. (although it doesn't really remove the file it simply [unlink](../devlog/unlink.md)s it, using professional software it is possible to recover files that were `rm`ed, to delete files safely [shred](../devlog/shred.md) should be used)   
   
   
- r`m -i` will ask before deleting each file. Some people will have `rm` [Aliases](/not_created.md) to do this automatically (type "alias" to check). Consider using `rm -I` instead, which will only ask once and only if you are trying to delete three or more files.   
- `rm -r` will recursively delete a directory and all its contents (normally rm will not delete directories, while rmdir will only delete empty directories).   
- `rm -f` will forcibly delete files without asking; this is mostly useful if you have rm aliased to `rm -i` but want to delete lots of files without confirming each one   
   
By default, when executed without any option, rm doesn’t remove directories and doesn’t prompt the user for whether to proceed with the removal of the given files.   
   
   
- To delete a single file, use the rm command followed by the file name as an argument:   
  - `rm filename`   
- If you don’t have write permissions on the parent directory, you will get “Operation not permitted” error.   
- If the file is not write protected, it will be removed without notice. On success, the command doesn’t produce any output and returns zero.   
   
Examples:   
   
   
- To remove non-empty directories and all the files within them recursively, use the -r (recursive) option:   
  - `rm -r dirname`   
- The -f option tells rm never to prompt the user and to ignore nonexistent files and arguments.   
  - `rm -f filename`   
- If you want to get information about what is being removed, use the -v (verbose) option:   
  - `rm -v filename`   
- You can use [regular expression](../devlog/regular%20expression.md)s to match multiple files. For example, to remove all .png files in the current directory, you would type:   
  - `rm *.png`   
- To remove one or more empty directories use the -d option:   
  - `rm -d dirname`   
  - `rm -d` is functionally identical to the [rmdir](/not_created.md) command.