---
created: 1661162245217
desc: ''
id: hehqr9nns2fwrvvjs8uhjjt
title: Deploy Nodejs Application
updated: 1661166923209
---
   
Deploy a [languages.javascript](../devlog/Nodejs.md) application on [DigitalOcean](../devlog/digitalocean.md).   
   
Steps:   
   
1. Create a Droplet.   
2. Write Ansible Playbook to:   
   
   - Install Node and NPM on the server.   
   - Copy Node artifact and unpack.   
   - Start application using Node command.   
   - Verify if app is running.   
   
   
---   
   
As a first step, create a Droplet on DigitalOcean, copy it's public IP address.   
   
**Write Playbook**   
   
   
- Add the public IP address of the server in the `hosts` file.   
   
```ini
<ip-address> ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_user=root
```
   
   
   
- Create a Playbook named `deploy-node.yml`   
   
```yaml
---
- name: Install Node & NPM
  hosts: <ip-address>
  tasks:
    - name: Update apt repo and cache
      # apt:
      #   update_cache: yes # or a oneliner
      apt: update_cache=yes force_apt_get=yes cache_valid_time=3600
    - name: Install nodejs & npm as a list
      # apt:
      #   name: nodejs
      #   state: present
      # apt: name=nodejs # also works but to install multiple pkgs
      apt:
        pkg:
          - nodejs
          - npm
# another play
- name: Deploy nodejs app
  hosts: <ip-address>
  tasks:
    # `npm pack` will return a .tgz file, when unpacked will have `package` dir.
    # `package` dir will have Dockerfile, Readme.md app dir, package.json
    # copy the pwd to .tgz
    # - name: Copy nodejs folder to the server
    #   copy:
    #     src: <path-to-nodejs>/nodejs-app.tgz
    #     dest: /root/app-1.0.0.tgz # root user home dir as logged in as root user
    # - name: Unpack .tgz
    #   unarchive:
    #     src: /root/app-1.0.0.tgz
    #     dest: /root/ # you can't specify a nested dir as it wouldn't have existed and by default it unpacks it wherever it's located
    #     remote_src: yes # if not mentioned unarchive will look for .tgz on the local machine
    - name: Unpack from local machine to remote machine
      unarchive:
        src: <path-to-nodejs>/nodejs-app-1.0.0.tgz
        dest: /root/
    # start nodejs app
    # install all dependencies
    # run the node command to start app/server.js
    - name: install dependencies
      npm:
        # path to package.json on remote
        path: /root/package/
    - name: start the application
      # command: node /root/package/app/server.js
      # command modules can be onliner or can be used with attributes
      command:
        chdir: /root/package/app/
        cmd: node server # will run perpetually and not let ansible playbook return
      # to continue execution of nodejs even after playbook completes we need to return it async-ly
      async: 1000
      poll: 0
    - name: Ensure app is running
      # pretty much same as command module but offers all the features that a shell has, but command is more secure, shell is more open to shell injection. Neither of them are idempotent.
      shell: ps aux | grep node
      # register; return values of modules and register it into variables.
      register: app_status
      # to reference the variable, of a task execution
    - debug: msg={{app_status.stdout_lines}} # msg={{app_status}}
```
   
   
As a security best practice you shouldn't run applications directly as the root user. You should create dedicated users for different applications with restrictive permissions.   
   
Refactoring Playbook following best security practices.   
   
```yaml
---
- name: Install Node & NPM
  hosts: <ip-address>
  tasks:
    - name: Update apt repo and cache
      apt: update_cache=yes force_apt_get=yes cache_valid_time=3600
    - name: Install nodejs & npm as a list
      apt:
        pkg:
          - nodejs
          - npm

- name: Create new linux user for node app
  hosts: <ip-address>
  tasks:
    - name: Create linux user
      user:
        name: ghost
        comment: a user named ghost 👻
        group: admin

- name: Deploy nodejs app
  hosts: <ip-address>
  # become_user = set to user with desired privileges Default is root.
  # become allows you to 'become' another user, different from the user that logged into the machine
  become: True # False by default
  become_user: ghost
  tasks:
    - name: Unpack from local machine to remote machine
      unarchive:
        src: <local-machine-path-to-nodejs>/nodejs-app-1.0.0.tgz
        dest: /home/ghost
    - name: install dependencies
      npm:
        path: /home/ghost/package/
    - name: start the application
      command:
        chdir: /home/ghost/package/app/
        cmd: node server
      async: 1000
      poll: 0
    - name: Ensure app is running
      shell: ps aux | grep node
      register: app_status
    - debug: msg={{app_status.stdout_lines}}
```
