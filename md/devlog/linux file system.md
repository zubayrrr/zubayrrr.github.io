---
created: '2021-10-13T00:00:00.000Z'
desc: ''
id: dgykbzysthli9tt1c7aj1f9
title: Linux File System
updated: 1652815514993
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- A file system controls how data is stored and retrieved.   
- Each group of data is called a file and the structure and the logic/rules used to manage files and their names are called file system.   
- A file system is a logical collection of files on a partition or disk.   
- On a Linux System, everything is considered to be a file and directory names are case-sensitive.   
- The Linux File System follows a "Tree" structure, there aren't any partitions but just one giant tree of directories.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.3ctr3rpzyao.png)   
   
   
---   
   
> The Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Linux distributions. It is maintained by the Linux Foundation. The latest version is 3.0, released on 3 June 2015. Linux distributions (and other operating systems) can voluntarily conform to the FHS.—via [filesystem hierarchy standard - Google Search](https://www.google.com/search?q=filesystem+hierarchy+standard&oq=filesystem+hi&aqs=chrome.1.69i57j0i512l5j0i22i30l4.8503j0j1&sourceid=chrome&ie=UTF-8)   
   
<table>   
<thead>   
<tr class="header">   
<th style="text-align: center;">Dir</th>   
<th>Description</th>   
</tr>   
</thead>   
<tbody>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2F" class="tc-tiddlylink tc-tiddlylink-missing">/</a></td>   
<td>The very top(root) of the file tree, holds everything else.</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Fbin" class="tc-tiddlylink tc-tiddlylink-missing">/bin</a></td>   
<td>Stores common Linux user command <a href="#Binaries" class="tc-tiddlylink tc-tiddlylink-missing">Binaries</a>, e.g. <code>date</code>,<code>cal</code> commands reside here</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Fboot" class="tc-tiddlylink tc-tiddlylink-missing">/boot</a></td>   
<td>Bootable <a href="#Linux%20Kernel" class="tc-tiddlylink tc-tiddlylink-missing">Linux Kernel</a> and <a href="#Bootloader" class="tc-tiddlylink tc-tiddlylink-missing">Bootloader</a> config files</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Fdev" class="tc-tiddlylink tc-tiddlylink-missing">/dev</a></td>   
<td>Files representing devices, tty=terminal, fd=floppydisk, (sd or hd) = <a href="#HDD" class="tc-tiddlylink tc-tiddlylink-resolves">HDD</a>s, ram = <a href="#RAM" class="tc-tiddlylink tc-tiddlylink-resolves">RAM</a>, cd = <a href="#CD-ROM" class="tc-tiddlylink tc-tiddlylink-missing">CD-ROM</a></td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Fetc" class="tc-tiddlylink tc-tiddlylink-missing">/etc</a></td>   
<td>Administrative Configuration files. The format for many of these configuration can be found in section 5 of <a href="#Man%20Pages" class="tc-tiddlylink tc-tiddlylink-resolves">Man Pages</a></td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Fhome" class="tc-tiddlylink tc-tiddlylink-missing">/home</a></td>   
<td>Where the home directories for regular users are stored. For example: <code>/home/user/</code></td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Fmedia" class="tc-tiddlylink tc-tiddlylink-missing">/media</a></td>   
<td>Unlike <a href="#%2Fdev" class="tc-tiddlylink tc-tiddlylink-missing">/dev</a>, <a href="#%2Fmedia" class="tc-tiddlylink tc-tiddlylink-missing">/media</a> is usually where removeable media(<a href="#USB" class="tc-tiddlylink tc-tiddlylink-resolves">USB</a> sticks, external <a href="#HDD" class="tc-tiddlylink tc-tiddlylink-resolves">HDD</a>s etc) are mounted</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Flib" class="tc-tiddlylink tc-tiddlylink-missing">/lib</a></td>   
<td>Contains shared libraries needed by applications in <a href="#%2Fbin" class="tc-tiddlylink tc-tiddlylink-missing">/bin</a> and <a href="#%2Fsbin" class="tc-tiddlylink tc-tiddlylink-missing">/sbin</a> to boot the system</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Fmnt" class="tc-tiddlylink tc-tiddlylink-missing">/mnt</a></td>   
<td>A place to mount external devices. This can still be used but has been superseded by <a href="#%2Fmedia" class="tc-tiddlylink tc-tiddlylink-missing">/media</a></td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Fmisc" class="tc-tiddlylink tc-tiddlylink-missing">/misc</a></td>   
<td>A directory used to sometimes automount filesystems on request</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Fopt" class="tc-tiddlylink tc-tiddlylink-missing">/opt</a></td>   
<td>Directory Structure used to store additional (i.e optional) software</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Fproc" class="tc-tiddlylink tc-tiddlylink-missing">/proc</a></td>   
<td>Information about System Resources</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Froot" class="tc-tiddlylink tc-tiddlylink-missing">/root</a></td>   
<td>The home folder for the root useraka the <a href="#superuser" class="tc-tiddlylink tc-tiddlylink-missing">superuser</a> (similar to the administrator on <a href="#Windows" class="tc-tiddlylink tc-tiddlylink-missing">Windows</a>)</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Fsbin" class="tc-tiddlylink tc-tiddlylink-missing">/sbin</a></td>   
<td>Contains administrative commands (binaries) for the root (super) user. In Ubuntu/Debian, <a href="#%2Fsbin" class="tc-tiddlylink tc-tiddlylink-missing">/sbin</a> and <a href="#%2Fbin" class="tc-tiddlylink tc-tiddlylink-missing">/bin</a> are <a href="#symlink" class="tc-tiddlylink tc-tiddlylink-resolves">symlink</a> to <a href="#%2Fusr" class="tc-tiddlylink tc-tiddlylink-missing">/usr</a><a href="#%2Fbin" class="tc-tiddlylink tc-tiddlylink-missing">/bin</a> and <a href="#%2Fusr" class="tc-tiddlylink tc-tiddlylink-missing">/usr</a><a href="#%2Fsbin" class="tc-tiddlylink tc-tiddlylink-missing">/sbin</a></td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Ftmp" class="tc-tiddlylink tc-tiddlylink-missing">/tmp</a></td>   
<td>Contains temporary files used by running applications.</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;"><a href="#%2Fusr" class="tc-tiddlylink tc-tiddlylink-missing">/usr</a></td>   
<td>Contains files pertaining to users that in theory don't change after installation.</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;"><a href="#%2Fvar" class="tc-tiddlylink tc-tiddlylink-missing">/var</a></td>   
<td>Contains directories of variable data that could be used by various applications. System log files are usually found here.</td>   
</tr>   
</tbody>   
</table>