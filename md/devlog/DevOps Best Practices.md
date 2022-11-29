---
created: 1654588644892
desc: ''
id: 5151o31s5jmalwws5joksse
title: DevOps Best Practices
updated: 1662903158474
---
   
   
- Use public key authentication for SSHing into servers.   
- Always create a new user (Do not use root user) on new machines. Add the user to the `sudo` group.   
- Create dedicated users for software like [jenkins](../devlog/jenkins.md), [nexus](../devlog/nexus.md) etc. Never run these services/software with root user permissions.   
- Never keep active access keys, generate them when you need it and simply delete them after use.   
- It is a good practice to run [Docker](../devlog/docker.md) containers with their own service user.   
- You should version your projects like using [version control.git](../devlog/version%20control.git.md) tags. A tag is like a branch that doesn't change.   
- What makes a good/senior DevOps engineer (among other things) is their ability to compare different tools and use the most efficient one to get the task done.   
- Always `chmod 400 ~/Downloads/key.pem` file.   
- 1 private 1 public subnet in each AZ. [aws](../devlog/aws.md)   
- It is a best practice to have all the code/configuration files in place with your application code. It may be a Jenkinsfile, Terraform, Ansible all in the same place as your application code.   
- Principle of least privilege - limits users' access rights to only what are strictly required to do their jobs.   
   
## Resources   
   
   
- [DevOps Best Practices | Atlassian](https://www.atlassian.com/devops/what-is-devops/devops-best-practices)