---
created: 20211030202952336
desc: ''
id: c75u8f4o0h0ych2bv2dswps
tags:
- TIL
title: Jack cannot support Bluetooth headphones
updated: 1652817950099
---
   
Topics::  [linux](../topics/linux.md), [music](../unsorted/music.md)   
   
   
---   
   
Jack cannot support Bluetooth headphones. Bluetooth headphone support is handled exclusively by PulseAudio (not even ALSA).   
   
The reason for Jack not supporting Bluetooth audio devices is primarily because Jack is for low latency professional audio, and Bluetooth adds a lot of latency. Basically, it's outside of the scope of the project altogether.   
   
> —via [Ubuntu Studio 19.04: How to use BlueTooth headphones with JACK? - Ask Ubuntu](https://askubuntu.com/questions/1151808/ubuntu-studio-19-04-how-to-use-bluetooth-headphones-with-jack)