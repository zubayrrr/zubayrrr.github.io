---
created: '2022-04-14T00:00:00.000Z'
desc: ''
id: zbxml2z2zzzsjj8eiagfzex
tags:
- tidbits
title: Create and Use Swap File on Linux
updated: 1652815514867
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- You can check it with the [free command in Linux](https://linuxhandbook.com/free-command/).   
   
```
free -h
```
   
   
   
- The free command gives you the size of the swap space but it doesn’t tell you if it’s a real swap partition or a swap file. The swapon command is better in this regard.   
   
```
swapon --show
```
   
   
### Step 1: Make a new swap file   
   
First thing first, create a file with the size of swap space you want. Let’s say that I want to add 1 GB of swap space to my system. Use the fallocate command to create a file of size 1 GB.   
   
```
sudo fallocate -l 1G /swapfile
```
   
   
It is recommended to allow only root to read and write to the swap file. You’ll even see warning like “insecure permissions 0644, 0600 suggested” when you try to use this file for swap area.   
   
```
sudo chmod 600 /swapfile
```
   
   
Do note that the name of the swap file could be anything. If you need multiple swap spaces, you can give it any appropriate name like swap_file_1, swap_file_2 etc. It’s just a file with a predefined size.   
   
### Step 2: Mark the new file as swap space   
   
Your need to tell the Linux system that this file will be used as swap space. You can do that with [mkswap](http://man7.org/linux/man-pages/man8/mkswap.8.html) tool.   
   
```
sudo mkswap /swapfile
```
   
   
You should see an output like this:   
   
```
Setting up swapspace version 1, size = 1024 MiB (1073737728 bytes)
no label, UUID=7e1faacb-ea93-4c49-a53d-fb40f3ce016a
```
   
   
### Step 3: Enable the swap file   
   
Now your system knows that the file swapfile can be used as swap space. But it is not done yet. You need to enable the swap file so that your system can start using this file as swap.   
   
```
sudo swapon /swapfile
```
   
   
Now if you check the swap space, you should see that your Linux system recognizes and uses it as the swap area:   
   
```
swapon --show
NAME       TYPE   SIZE USED PRIO
/swapfile  file 1024M   0B   -2
```
   
   
### Step 4: Make the changes permanent   
   
Whatever you have done so far is temporary. Reboot your system and all the changes will disappear.   
   
You can make the changes permanent by adding the newly created swap file to /etc/fstab file.   
   
It’s always a good idea to make a backup before you make any changes to the /etc/fstab file.   
   
```
sudo cp /etc/fstab /etc/fstab.back
```
   
   
Now you can add the following line to the end of /etc/fstab file:   
   
```
/swapfile none swap sw 0 0
```
   
   
You can do it manually using a [command line text editor](https://itsfoss.com/command-line-text-editors-linux/) or you just use the following command:   
   
```
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
   
   
Now you have everything in place. Your swap file will be used even after you reboot your Linux system.