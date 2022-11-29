---
created: 20211027091606516
desc: ''
id: slwkpjzurunu7jlsa4wcj9y
title: File Permissions
updated: 1653683915153
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- File Permissions (file modes) specify who can access, change or execute a file on a Linux System   
- It ensures that only authorized users and processes can access files and directories   
- Each file or directory has an owner and a [group](/not_created.md). By default, the owner is the user who creates the file and the group is the primary group of that user   
- The ownership of a file or a directory can be changed only by root using the [chown](../devlog/chown.md) and `chgrp` commands   
   
### For each file the permissions are assigned to three different categories of users:   
   
1.  The File owner   
2.  The Group owner   
3.  Others (anyone else or the whole world)   
   
### There are three file permissions types that apply to each category:   
   
   
- The read permission (r)   
- The write permission (w)   
- The execute permission (x)   
   
### To view the files permissions run: [ls](../devlog/ls.md) -l or [stat](../archive/STAT.md)   
   
   
- `-` indicates the absence of a permission   
- The order of permissions is `FileType` denoted with `d`, `l`, `-` etc followed by permissions for the user in the format `rwx` followed by permissions for the group followed by permissions for other users   
- `root` user can always `rwx` because permissions are always only for non-privileged users.   
- `x` all Linux commands or shell scripts have the `x` permission set. If a file that represents a command doesn't have `x` permission it cannot be executed.   
   
### Combining Find and Chmod Commands Together   
   
To recursively set permissions for all files to a specific value, you should exclude the directories in the path otherwise the directories will have same permissions as the files, see: [The Effect of Permissions on Directories](../devlog/the%20effect%20of%20permissions%20on%20directories.md)   
   
To mitigate this, we can combine [find](../devlog/find.md) and [chmod](../devlog/chmod.md) commands together   
   
Example   
   
   
- `find ~ -type f -exec chmod 640 {} \;` for all files   
- `find ~ -type d -exec chmod 750 {} \;` for all directories   
   
### Changing File Ownership   
   
   
- In Linux, all files are associated with an owner and a group owner   
- The [chown](../devlog/chown.md) and `chgrp` commands are used to change the files owner and group   
- Only root can change the file owner   
- Normal users can change the group of the file if they own the file and only to a group of which they are member of root can change the group ownership of all files.   
   
   
---   
   
### Special Permissions   
   
   
- Besides `r`, `w` and `x` for the owner, group and others there are 3 extra special permissions for each file or directory:   
  - [suid](../devlog/suid.md) or Set User ID   
  - [SGID](../devlog/sgid.md) or Set Group ID   
  - [Sticky Bit](../devlog/sticky%20bit.md)   
- These special permissions are for the file or directory overall, not just for a user category.   
   
### Special Permission - [suid](../devlog/suid.md)   
   
   
- **When an execuatable file with [suid](../devlog/suid.md) is executed then the resulting process will have the permissions of the owner of the command, not the permissions of the user who executes the command**.   
- Sometimes it is necessary for a system to temporarily treat a user as root which is where [suid](../devlog/suid.md) comes into play.   
  - [passwd](../devlog/passwd.md) command has SUID set by default so that even nonpriviledged users can change their password.   
- Absolute Mode: `chmod 4xxx file`   
- Relative Mode: `chmod u+s file`   
- `ls -l /usr/bin/passwd`   
  - `-rwsr-xr-x 1 root root 68208 apr 16 15:36` /usr/bin/passwd   
   
For example:   
   
`cat` will only be able to read a file if the user has the permissions to read the file.   
   
`ls -l /usr/bin/cat` the owner of the executable is `root` but it'll be run as per the privileges of the user that invokes the command.   
   
In case of `/etc/shadow` file, `cat` will not be able to read the contents because it doesn't yet have the [suid](../devlog/suid.md) `s` set for it, so its not able to inherit the permissions of the `root`, even though `root` is the owner of the command `cat` but since [suid](../devlog/suid.md) is not set, it is inherting the permissions of the nonprivileged user.   
   
If there is a `0` before the numeric value for "Access" when you run [stat](../archive/STAT.md) on a file, it means there are no special permissions set for that file.   
   
### Setting up SUID   
   
`sudo chmod 4755 /usr/bin/cat` using [chmod](../devlog/chmod.md) setting the [suid](../devlog/suid.md) and checking with `ls -l /usr/bin/cat` will return `-rwsr-xr-x` with /usr/bin/cat in red(or different) color.   
   
If you check with [stat](../archive/STAT.md) command you'll find "Access" with the value: `4755`   
   
Sometimes you'll find an uppercase `S` instead of a lowercase `s` denoting that there are no `x` executable permissions for that file.   
   
#### SUID with symbolic mode   
   
`sudo chmod u+s /usr/bin/cat`   
   
### Finding all the commands with the SUID set   
   
`find /usr/bin -perm -4000` [find](../devlog/find.md)   
   
### Special Permission - [SGID](../devlog/sgid.md)   
   
   
- SGID or Set Group ID   
- SGID is set mainly to directories   
- If you set SGID on directories, all files or directories created inside that directory will be owned by the same group owner of the directory where SGID was configured.   
- This is useful in creating shared directories, which are directories that are writable at the group level.   
- Absolute Mode: `chmod 2xxx directory`   
- Relative Mode: `chmod g+s directory`   
- `ls -ld /programming/`   
  - `drwxrws---2 pr1 programmers 4096 iul 14 13:15 /programming/`   
   
For example:   
   
   
- `sudo su`   
- `groupadd programmers`   
- `useradd -s /bin/bash pr1`   
- `useradd -s /bin/bash pr2`   
- `usermod -aG programmers pr1`   
- `usermod -aG programmers pr2`   
- `mkdir /programming/`   
- `chown pr1:programmers /programming/`   
- `chmod 770 /programming/`   
- `su pr1`   
- `cd /programming/`   
- `touch source1.cpp`   
   
At this point the <span class="underline">group owner of the file is the primary group of the creator</span> and the other users in the `programmers` group will not be able to change the file or work on it, we can give individual permissions to the other users but it can be a security issue.   
   
### Setting up SGID   
   
`chmod 2770 /programming` or `chmod g+s /programming`   
   
Verify with `ls -ld /programming` or `stat /programming`   
   
There will be an additional `s` letter added to the permissions, if there is an uppercase `S` it means there are not execution permissions set for that directory.   
   
   
- `su pr2`   
- `cd /programming`   
- `touch source2.cpp`   
- `mkdir goland python`   
  - Newly created dirs will have similar permissions as the parent directory with the SGID set   
- The group of the newly created files and dirs will be "programmers" and not "pr1"   
   
   
---   
   
### File Attributes   
   
### File Attributes   
   
   
- A part from permissions Linux also has advance access control features such as [ACL](/not_created.md)s and attributes.   
- The attributes define the properties of the files, they depend on the underlying file system such as [ext4](/not_created.md) where the attribute data must be stored along with other control structures.   
- Each file attribute can have one of the two states: `set` or `clear`   
- Attributes is separate from other metadata such as file system permissions, owners, groups, timestamps and so on.   
- [ls](../devlog/ls.md) doesn't display the file attributes, use [lsattr](../devlog/lsattr.md) for that and to change attributes use [chattr](../devlog/chattr.md)   
   
See also:   
   
   
- [Octal Notation](../devlog/octal%20notation.md)   
- [chmod](../devlog/chmod.md), [chown](../devlog/chown.md), [chmod](../devlog/chmod.md), [chgrp](../devlog/chgrp.md)   
- [umask](../devlog/umask.md)   
- [The Effect of Permissions on Directories](../devlog/the%20effect%20of%20permissions%20on%20directories.md)   
- [lsattr](../devlog/lsattr.md), [chattr](../devlog/chattr.md)