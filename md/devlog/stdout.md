---
created: '2021-10-11T00:00:00.000Z'
desc: ''
id: do68y261xeu98bpq3vl5cn9
title: stdout
updated: 1652947243111
---
   
   
- It is part of [Standard Data Stream](../devlog/standard%20data%20stream.md)   
- [stdout](../devlog/stdout.md) is denoted by the number 1 in the [Standard Data Stream](../devlog/standard%20data%20stream.md)   
- Example of changing destination of [stdout](../devlog/stdout.md): `cat 1> output.txt`   
- Where `1` is the number of data stream `>` is direction and `output.txt` is destination. (note that we cannot add a space after `1` or before the `>` sign)   
- Alternatively you can skip the `1` because Linux by default is expecting [stdout](../devlog/stdout.md) so just do: `cat > output.txt`   
- To avoid truncation (overwriting), you can use `>>` example:     
  `cat >> output.txt` and now whenever you try to redirect [stdout](../devlog/stdout.md), it'll append instead of truncating.   
   
- Example: `date >> date.md`