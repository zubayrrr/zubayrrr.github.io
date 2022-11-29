---
created: 20210927100508868
desc: ''
id: mlkhrpx7izin3fiwgsz9d68
title: QR Code
updated: 1663212742028
---
   
Topics::  [computer science](../topics/computer%20science.md)   
   
   
---   
Quick Response(QR) codes can store more information such as URLs, SMS, text messages, coupons, they're a series of squares that allows us to store more information from a [Barcode](../devlog/barcode.md).   
   
   
---    
   
# [QR codes | Dan Hollick 🇿🇦](https://typefully.com/DanHollick/qr-codes-T7tLlNi)   
   
Ever wondered how a QR code works? No, me neither but it's low-key fascinating. (Warning, there is some extremely nerdy shit here.👇 )   
   
![](https://api.typefully.com/media-p/b01954fa-0025-465c-b349-7046a79852e5/)   
   
The Quick Response code was invented by a subsidiary of Toyota to track parts across the manufacturing process. Barcodes were proving inadequate - they can only be read at certain angles and didn't store much data relative to their size The QR code solves those issues and more   
   
![](https://api.typefully.com/media-p/5a668798-d619-4e47-a6cd-e80b552e59ee/)   
   
The most distinctive thing about a QR code are these cube shapes, called Finder Patterns, that help your reader detect the code. The smaller fourth cube, the Alignment Pattern, orientates the code so it can be at any angle and the reader will still know which way is up.   
   
![](https://api.typefully.com/media-p/fa7a9107-8dba-464c-bb48-15668e5342c0/)   
   
You've probably never noticed but every QR code has these alternating black and white dots called the Timing Pattern. These tell the reader how big a single module is and how big the whole QR code is - known as the version. Version 1: Smallest Version 40: Biggest   
   
![](https://api.typefully.com/media-p/836d3a95-1c1e-4445-897e-d7dbaa591050/)   
   
![](https://api.typefully.com/media-p/2107ff0f-c051-493c-b4d3-275d2da3c9ed/)   
   
Information about the format is stored in these two strips near the Finder patterns. It's stored twice so its readable even when QR code is partially obscured. (You'll notice that this is a recurring theme.)   
   
![](https://api.typefully.com/media-p/0c0a45ac-47bb-4e68-b158-6beec3a304cc/)   
   
This stores three crucial pieces of information: - Mask. - Error correction level - Error correction format. I know these sound super fucking boring but they are actually pretty interesting.   
   
![](https://api.typefully.com/media-p/4a203e8e-65d1-4068-8741-c87737f3c581/)   
   
First, error correction - what is it? Essentially, it dictates how much redundant information is stored in the code to ensure it remains readable even when part of it is missing.   
   
![](https://api.typefully.com/media-p/946c1de6-ac0e-42d7-b580-b0800a22c379/)   
   
This is pretty amazing - If your code is outdoors you can choose a higher redundancy level to make sure it still functions when obscured. (try it)   
   
![](https://api.typefully.com/media-p/ebd1a3af-fb6b-4e60-91c7-fd4ffc56c317/)   
   
Second, the mask - what's that? Well, QR readers work best when there are the same amount of white and black areas. But the data might not play ball so a mask is used to even things out.   
   
![](https://api.typefully.com/media-p/8be3fffa-1ddc-4229-b2b3-64a8a1e2833a/)   
   
When a mask is applied to the code anything that falls under the dark part of the mask is inverted. A white area becomes black and black area becomes white.   
   
![](https://api.typefully.com/media-p/d52e6088-3f15-4d91-b892-8eb37b95bbc5/)   
   
There are 8 standard patterns which are applied one by one. The pattern that achieves the best result is used and that info is stored so the reader can unapply the mask.   
   
![](https://api.typefully.com/media-p/81ad5b5b-8de0-4094-b553-93433576d08e/)   
   
Finally we get to the actual data. Weirdly, the data starts at the bottom-right corner and winds back up like pictured. It almost doesn't matter where it starts because it can be read at any angle.   
   
![](https://api.typefully.com/media-p/fe8d2686-a217-45da-93f1-351cfc025fb8/)   
   
The first chunk of information here tells the reader what mode the data was encoded in and the second tells it the length. In our case each character takes up 8 bit chunks, otherwise known as bytes, and there are 24 of them.   
   
![](https://api.typefully.com/media-p/dc90f7ce-8d0a-4e3a-aef7-943afe1644fb/)   
   
There is still a bunch of left over space after our data. This is where the error correction information is stored so that it can be read if partially obscured. The way this works is actually really really complex so I'll leave that out. That's basically it!   
   
![](https://api.typefully.com/media-p/305cd254-243f-4e43-b184-2d6163adb1de/)   
   
For the absolute nerds who made it here, a fun fact: Perhaps the coolest thing about QR codes is that Denso Wave, the company that invented them, never exercised their patent and released the technology for free! [https://www.denso-wave.com/en/technology/vol1.html](https://www.denso-wave.com/en/technology/vol1.html)