---
created: 1656562183828
desc: ''
id: jicnn49265p0krb9cmh4v3x
title: Wireshark
updated: 1656564532783
---
   
Wireshark is one of the best network protocols for analyzing freely available packages. Previously known as Ethereal, Wireshark is widely used by industries and educational institutes. Wireshark has a “live capturing” ability for packet investigation, and the output data is stored in XML, CSV, PostScript, and plain text documents. This program is the most famous network protocol analyzer, and its purpose is to see what is happening around your network. Wireshark provides all the details you need to know about the packets in movement in your network.   
   
## Features   
   
Wireshark contains several useful features, the foremost of which are listed below:   
   
   
- Inspecting thousands of protocols   
- New protocols being added with every update   
- Live-capturing of protocols with offline analysis   
- Three-way handshake   
- Maximum portability: runs on Solaris, Linux, Windows, MAC OS X, FreeBSD, and more   
- Analyzing VoIP protocols   
- Reads data from many platforms, i.e., Wi-Fi, Ethernet, HDLC, ATM, USB, Bluetooth, Frame Relay, Token Ring, and more   
- Results can be saved in CSV, XML, PostScript, and plain text documents   
- Reads and write a wide variety of captured file formats   
   
## Lab   
   
   
- Wireshark captures data from network interface.   
  - You specify the interface where you want to capture data from.   
- When you want to capture data from a network that is not yours(you're not part of) you need a network interface card that can be put into monitor(or promiscuous) mode.   
   
1. Start your wireshark: `sudo wireshark`   
2. Select the Network Interface you want to capture from   
   
	![](https://res.cloudinary.com/zubayr/image/upload/v1656564583/wiki/fq6qfmktq5g307dfd2hp.png)   
   
3. Wireshark will start capturing data   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656564634/wiki/vkhseens6nesk0jpc80c.png)   
   
4. As we know that data is called by different names at different layers, for example frames, packets etc.   
5. Select a frame from the frame list   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656564941/wiki/mogpgsv01imjawha3unt.png)   
   
We can see information about this particular frame, it’s source and destination IP, in this case it seems like the request was sent to my Samsung device.   
   
Below in the packet bytes menu, we can also see that the data is in scrambled state(hexdecimal and ASCII).   
   
You can even view the data in bits(binary). Right click and convert the data into your desired format.   
   
6. Analyzing a layer 7 packet   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656566188/wiki/y8xnjecfoiu6lswkfinz.png)   
   
We can see that this was an HTTP frame, it originated from what application(qBittorrent), we see that our target is doing some shady torrenting.   
   
Let’s see if we can follow this stream and check what they actually got.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656566302/wiki/qoxgwp5afttglbg2yk88.png)   
   
It looks like this particular HTTP GET request sent back some data - it’s not really HTML, like you’d expect(?).   
   
You can save all the captured traffic in a `.pcap` file and try to analyze the traffic, put the captured traffic back into it’s original state etc.