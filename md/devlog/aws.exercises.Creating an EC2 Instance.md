---
created: 1664916323752
desc: ''
id: qy0tk95w2ji6dy8dfnsxwtn
title: Creating an EC2 Instance
updated: 1664917197858
---
   
   
- Create an [aws.EC2](../devlog/aws.EC2.md) instance   
  - Instance type: t2.micro   
  - Amazon Machine Image (AMI): Amazon Linux 2   
  - Default options for everything else   
  - Create and save the key pair   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664917152/wiki/jwfp8mfagibagxhc2anl.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664917320/wiki/iiifkqvmmemfwxrvhuvj.png)   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664917259/wiki/ocv6kbwhweqo9aybmop5.png)   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664917366/wiki/ljtafi5ayhug6irphplq.png)   
   
Connect to the newly created instance using the `.pem` file.   
   
```bash
ssh -i ~/Downloads/aws-t2-micro.pem  ec2-34-228-73-4.compute-1.amazonaws.com
```
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664917656/wiki/yfttnmwny05qrbigh6h7.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664917681/wiki/q4v3r2sof9cncan3ilmw.png)   
   
Change permissions of the `.pem`   
   
```shell
sudo chmod 600 /path/to/my/key.pem 
```
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664917803/wiki/klpljoj50dfirastcbr2.png)   
   
oops forgot to add the user `ec2-user` before the address   
   
`cd ~/path/to/.pem`   
   
```bash
ssh -i "aws-t2-micro.pem" ec2-user@ec2-34-228-73-4.compute-1.amazonaws.com
```
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664918767/wiki/nukjtlubutxegv4mw5ko.png)   
   
and we’re in.   
   
Make sure to destroy it once you’re done using it.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664918849/wiki/rkfx7ag3hmhossnqr0ay.png)   
   
## Optionally, you can also add a security group   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664930776/wiki/ckcq2wvzbkv5xch4mtqj.png)