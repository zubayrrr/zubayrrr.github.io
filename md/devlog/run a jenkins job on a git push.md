---
created: 1660673979767
desc: ''
id: hzd9fv7vfkvzzvziuo81jtk
title: Run a Jenkins Job on a Git Push
updated: 1660674729363
---
   
## Let's configure an automatic trigger of a Jenkins Job on a [version control.git](../devlog/version%20control.git.md) push.   
   
1. From "Manage Plugins" page install `Gitlab` for build triggers.   
2. From "Manage Jenkins" page -> "Configure System", find “Gitlab” section   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660674209/wiki/xdqlghfvcdwvf37ncrwe.png)   
   
3. Configure a Gitlab Connection   
   
   - Use Gitlab API Token(Personal Access Token)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660674456/wiki/oa8vjoyc8gfntpit0k0w.png)   
   
4.  A GitLab connection will now appear on your pipelines’ config page and the option for building on a push to GitLab repository   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660674626/wiki/sp0aoficzpvmpvq4rozm.png)   
   
The same options are available once GitLab connection is added on a freestyle job as well.   
   
5. Go to Gitlab(`repository-name/settings/integrations`) to find “Jenkins CI” to configure Gitlab to send a notification to Jenkins whenever a push is made.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660675011/wiki/fqvrsg30mjmgur8ubtb3.png)   
   
6. Save settings and Test settings   
   
   
---   
   
## Let’s configure automatic triggering of Jenkins job on a multibranch pipeline.   
   
The steps done for a regular pipeline cannot be applied to multibranch pipeline (Gitlab connection and options will appear but they’ll be in read-only mode).   
   
1. From Plugin Manager install “Multibranch Scan Webhook Trigger”.   
2. Go to config page on your multibranch  pipeline.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660675679/wiki/mwdw8cjo7z9o8vdqaz9u.png)   
   
   
3. Enable “Scan by webhook”    
4. Add a Trigger Token name(can be anything)   
5. Go to Gitlab(`repository/hooks`) webhooks   
6. Configure Gitlab to send a notification on a specific URL (Jenkins URL)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660675712/wiki/bom1cka6abihnilouuly.png)   
   
7. Add webhook once done configuring.