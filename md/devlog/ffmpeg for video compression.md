---
created: '2021-10-19T00:00:00.000Z'
desc: ''
id: arydcbu4rt16unw2u498k1t
tags:
- tidbits
title: ffmpeg for Video Compression
updated: 1652815757434
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Note that it seems that ffmpeg already performs some optimization when ran without options, so before trying to use settings you don't understand or deciding to explicitly lose information, give a try to a default conversion :   
   
`ffmpeg -i input.mp4 output.mp4`   
   
In my case it reduced the bitrate of both the video and audio (you can check and compare the input and output file by running ffprobe on them), transforming a 700 Mb video into a 60 Mb one of seemingly similar quality.   
   
> —via [How can I reduce a video's size with ffmpeg? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/28803/how-can-i-reduce-a-videos-size-with-ffmpeg)