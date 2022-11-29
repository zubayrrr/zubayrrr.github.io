---
created: '2022-03-29T00:00:00.000Z'
desc: ''
id: mut65xusg0h2quvskzdyral
tags:
- tidbits
title: pulseaudio bluetooth module missing
updated: 1652815757668
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
```bash
sudo apt-get install pulseaudio-module-bluetooth
sudo killall pulseaudio
pulseaudio --start
sudo systemctl restart bluetooth
```
   
   
Adding the module-bluez5-discover at the end of the pulseaudio `/etc/pulse/default.pa` config:   
`load-module module-bluez5-discover`   
   
> — via [bluetooth - a2dp-sink profile connect failed - Ask Ubuntu](https://askubuntu.com/questions/1172000/a2dp-sink-profile-connect-failed)   
   
   
---   
   
First, let’s check whether we have all the dependencies installed:   
`sudo apt install pulseaudio pulseaudio-utils pavucontrol pulseaudio-module-bluetooth`   
When we verify it, we need to create or edit this audio config file:   
`sudo gedit /etc/bluetooth/audio.conf`   
Include the next lines:   
This section contains general options   
   
```
[General]
Enable=Source,Sink,Media,Socket
```
   
   
> In most cases the first thing we do after we boot up our system is turning on the Bluetooth headset. Sometimes the system and the device pair up well but no sound. If you use the command journalctl -f you will receive the next message:   
> — via [Common Bluetooth Problems in Ubuntu and How to Fix Them - DEV Community](https://dev.to/campbelljones74/common-bluetooth-problems-in-ubuntu-and-how-to-fix-them-18b5)