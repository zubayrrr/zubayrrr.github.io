---
created: '2022-05-14T00:00:00.000Z'
desc: ''
id: mx45kfy1ylv6jtvjxsomm0o
title: dd
updated: 1653306004697
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
**dd** is a command-line utility whose primary purpose is to convert and copy files.   
   
Compared to the [cp](../devlog/cp.md) command, `dd` is used read and write from special device files. `dd` is a powerful tool with drive erasing capability.   
   
<blockquote class="quoteback" darkmode="" data-title="How%20to%20use%20dd%20in%20Linux%20without%20destroying%20your%20disk" data-author="" cite="https://opensource.com/article/18/7/how-use-dd-linux">   
                      "<em>dd</em> stands for <em>disk destroyer</em>."   
                      <footer> <cite><a href="https://opensource.com/article/18/7/how-use-dd-linux">[https://opensource.com/article/18/7/how-use-dd-linux</a></cite></footer>](https://opensource.com/article/18/7/how-use-dd-linux</a></cite></footer>)   
                      </blockquote>   
   
`if=` defines the source drive (input file) and `of=` defines the file or location where you want your data saved(output file).   
   
```
dd if=/dev/sda of=/dev/sdb
```
   
   
create an .img archive of the ` /dev/``sda ` drive and save it to the home directory of your user account   
   
```
dd if=/dev/sda of=/home/user/sdadisk.img

# with status

dd if=/dev/sda of=/home/user/sdadisk.img status=progress
```
   
   
`dd` works with blocks and will infact clone the device by coping everything both empty and occupied space.   
   
If you want to restore a disk with the `.img` file; just use the `.img` file as the input (`if`) and the disk or partition as the destination (`of`)   
   
```
dd if=/home/username/sdadisk.img of=/dev/sda status=progress
```
   
   
You can also use `sync` option using synchronised input out   
   
```
dd if=/home/username/sdadisk.img of=/dev/sda status=progress conv=sync
```
   
   
## Copying only the [MBR](/not_created.md) block or `mbr.dat` file   
   
```
sudo dd if=/dev/sda of=/root/mbr.dat bs=512 count=1
```
   
   
## Restoring the [MBR](/not_created.md) using `mbr.dat`   
   
```
sudo dd if=/root/mbr.dat of=/dev/sda bs=512 count=1
```
   
   
## Create Bootable USB stick using `dd`   
   
   
- unmount if its already [mount](../devlog/mount.md)ed using [umount](../devlog/umount.md) command   
   
```
umount /media/user/device-name
```
   
   
   
- format the disk using [mkfs](/not_created.md)   
   
```
mkfs.vfat /dev/sdb
```
   
   
   
- using `dd` to copy the `.iso` file   
   
```
sudo dd if=/home/user/Downloads/linuxmint.iso of=/dev/sdb bs=4M status=progress
```
   
   
## Footnotes   
   
To add fancier progress/status monitor , use [pv](/not_created.md) or Pipe Viewer