---
created: 1664934526447
desc: ''
id: pb867vhj1io7ehtr834v8zq
title: Deploy a Node Application on EC2
updated: 1665005741099
---
   
Related::  [aws.ec2](../devlog/aws.EC2.md)   
   
   
---   
   
   
- Install Git   
   
```bash
sudo yum update -y
sudo yum install git -y
```
   
   
   
- [Setting Up Node.js on an Amazon EC2 Instance](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html)   
   
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
. ~/.nvm/nvm.sh
nvm install --lts
```
   
   
   
- Clone the project using [version control.git](../devlog/version%20control.git.md) or you can copy it from your local machine using [scp](../devlog/scp.md)   
   
We'll be using [ryanmurakami/fieldday](https://github.com/ryanmurakami/fieldday) repo.   
   
```
git clone https://github.com/ryanmurakami/fieldday
cd fieldday
npm install
npm run start
```
   
   
You can now access your application running on port 3000 (if you've opened this port as a security policy of the EC2 instance) on your instance's Public IPv4 DNS:3000   
   
such as: `http://ec2-3-86-99-185.compute-1.amazonaws.com:3000/`   
   
   
---   
   
## Specify instance user data at launch   
   
Under Advanced Details on instance launcher page add the user data(script)   
   
```bash
#!/bin/bash
touch ~/.bashrc
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
source ~/.bashrc
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
nvm install --lts
sudo yum update -y
sudo yum install git -y
git clone https://github.com/ryanmurakami/fieldday
cd fieldday
npm install
npm run start
```
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664987819/wiki/wtqbghrzmtehpetoex4r.png)   
   
   
- Check the log of your user data script in:   
   
`/var/log/cloud-init.log` and   
`/var/log/cloud-init-output.log`   
   
Or check the log from   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1664987877/wiki/jc7f0q1hzahdxoj6zf7n.png)