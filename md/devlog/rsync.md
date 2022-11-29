---
created: '2022-03-26T00:00:00.000Z'
desc: ''
id: dlwsd1h4qr9cqep4z0jw8vd
title: rsync
updated: 1652817053135
---
   
Topics::  [linux](../topics/linux.md), [networking](../topics/networking.md)   
   
   
---   
   
The `rsync` utility expressions take the following form:   
   
```sh
Local to Local:  rsync [OPTION]... [SRC]... DEST
Local to Remote: rsync [OPTION]... [SRC]... [USER@]HOST:DEST
Remote to Local: rsync [OPTION]... [USER@]HOST:SRC... [DEST]
```
   
   
Copy   
   
   
- `OPTION` - The rsync options .   
- `SRC` - Source directory.   
- `DEST` - Destination directory.   
- `USER` - Remote username.   
- `HOST` - Remote hostname or IP Address.   
   
`rsync` provides a number of options that control how the command behaves. The most widely used options are:   
   
   
- `-a`, `--archive`, archive mode, equivalent to `-rlptgoD`. This option tells `rsync` to syncs directories recursively, transfer special and block devices, preserve symbolic links, modification times, groups, ownership, and permissions.   
- `-z`, `--compress`. This option forces `rsync` to compresses the data as it is sent to the destination machine. Use this option only if the connection to the remote machine is slow.   
- `-P`, equivalent to `--partial --progress`. When this option is used, `rsync` shows a progress bar during the transfer and keeps the partially transferred files. It is useful when transferring large files over slow or unstable network connections.   
- `--delete`. When this option is used, `rsync` deletes extraneous files from the destination location. It is useful for mirroring.   
- `-q`, `--quiet`. Use this option if you want to suppress non-error messages.   
- `-e`. This option allows you to choose a different remote shell. By default, `rsync` is configured to use ssh.   
   
## Basic Rsync Usage   
   
The most basic use case of `rsync` is to copy a single file from one to another local location. Here is an example:   
   
```bash
rsync -a /etc/ ~/etc_backup/
```
   
   
The user running the command must have read permissions on the source location and write permissions on the destination.   
   
Omitting the filename from the destination location copies the file with the current name. If you want to save the file under a different name, specify the new name on the destination part:   
   
```
rsync -a /opt/filename.zip /tmp/newfilename.zip
```
   
   
The real power of `rsync` comes when synchronizing directories. The example below shows how to create a local backup of website files:   
   
```
rsync -a /var/www/domain.com/public_html/ /var/www/domain.com/public_html_backup/
```
   
   
If the destination directory doesn’t exist, `rsync` will create it.   
   
It is worth mentioning that `rsync` gives different treatment to the source directories with a trailing slash (`/`). If the source directory has a trailing slash, the command will copy only the directory contents to the destination directory. When the trailing slash is omitted, `rsync` copies the source directory inside the destination directory.   
   
   
---   
   
## Using rsync Over the Network   
   
When using `rsync` to [transfer data remotely , it must be installed on both the source and the destination machine. The new versions of `rsync` are configured to use SSH as default remote shell.   
   
In the following example, we are transferring a directory from a local to a remote machine:   
   
```
rsync -a /opt/media/ remote_user@remote_host_or_ip:/opt/media/
```
   
   
or   
   
```
rsync -av -e ssh /etc/ remote_user@remote_host_or_ip:~/etc_bacup/
```
   
   
To transfer data from a remote to a local machine, use the remote location as a source:   
   
```
rsync -a remote_user@remote_host_or_ip:/opt/media/ /opt/media/
```
   
   
If SSH on the remote host is listening on a port other than the default 22 , specify the port using the `-e` option:   
   
```
rsync -a -e "ssh -p 2322" /opt/media/ remote_user@remote_host_or_ip:/opt/media/
```
   
   
There are two options to exclude files and directories. The first option is to use the `--exclude` argument and specify the files and directories you want to exclude on the command line.   
   
When excluding files or directories , you need to use their relative paths to the source location.   
   
In the following example shows how exclude the `node_modules` and `tmp` directories:   
   
```
rsync -a --exclude=node_modules --exclude=tmp /src_directory/ /dst_directory/
```
   
   
The second option is to use the `--exclude-from` option and specify the files and directories you want to exclude in a file.   
   
```
rsync -a --exclude-from='/exclude-file.txt' /src_directory/ /dst_directory/
```
   
   
```bash
$ cat exclude-file.txt
node_modules
tmp
```
   
   
> via - [Rsync Command in Linux with Examples | Linuxize](https://linuxize.com/post/how-to-use-rsync-for-local-and-remote-data-transfer-and-synchronization/)