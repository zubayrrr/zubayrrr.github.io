---
created: 1653430100223
desc: ''
id: mwyyxjbpi0gztjd00f39biv
title: Ansible
updated: 1665172390874
---
   
Topics::  [devops](../topics/devops.md)   
Related::  [puppet](../devlog/puppet.md), [chef](../devlog/chef.md)   
   
   
---   
   
Ansible is a tool that helps you automate certain IT tasks that are better taken care of in an automated fashion. Example:   
   
   
- Running an distributed application across 10 servers, let say you've a new version to deploy, Ansible comes into play here.   
- Updating Docker or other applications running on your servers.   
- Scheduled or manual backups.   
- Weekly system reboot.   
- Creating users, assigning permissions etc.   
   
   
---   
   
**Why use Ansible?**   
   
   
- Execute tasks from your own machine(remotely without having to [ssh](../devlog/ssh.md) into a multiple machines and running a task one by one)   
- Configuration/Installation/Update/Deployment steps all laid in a single [languages.YAML](../devlog/languages.YAML.md) file.   
- Re-use the [languages.YAML](../devlog/languages.YAML.md) file multiple times if needed on the same server/environment or different.   
- More reliable and less likely for errors, less prone to human error.   
- It supports all operating systems, different cloud providers, works with virtual cloud server or bare metal infra.   
   
   
---   
   
   
- Ansible is a configuration management system used to configure, automate,monitor, and troubleshoot devices in large networks.   
- It is written in [languages.python](../devlog/languages.python.md) and is open source under GPL License.   
- There is a control node and many managed nodes (network devices we manage with Ansible). Windows OS is not supported as a control node at this moment (only [WSL](/not_created.md));   
- Ansible uses an **agentless** architecture. No application is installed on the managed nodes and no daemon, process or agent is running.   
  - No deployment effort in the beginning or no upgrade effort when moving to a new Ansible version.   
- Ansible uses for device configuration. Any system that can be configured using [SSH](../devlog/ssh.md) can also be configured using Ansible;   
- When managing Windows it users native PowerShell remote support instead of SSH;   
- It is also known as an orchestration engine, used in large networks with many devices that need to be configured, maintained and troubleshooted in an automated way.   
- Ansible uses Modules which are scripts or units of work that do the actual job.   
- Theres no process that runs continuously on neither the controlling machine or the managed machine(s)   
- The controlling node doesn't have be a privileged user, it can simply ssh into the managed node.   
   
## Ansible Components/Architecture   
   
   
- Ansible uses [languages.YAML](../devlog/languages.YAML.md).   
   
### Modules Overview   
   
   
- Modules are the units of code ansible executes. Each module has a particular use, from administering users on a specific type of database to managing VLAN interfaces on a specific type of network device or to installing, configuring and starting a specific server like for example Apache2 on a Linux distribution.   
  - They get sent from control machine to the target server. They do their job(like install an application, apply firewall rules etc ) and once they're done, they're removed.   
  - Modules are very granular. One module does one small task. Such as: a module to copy a file, module to install an Ngnix server, to start the Ngnix server etc.   
  - Ansible has hundreds of modules that each execute a specific task.   
  - Ansible also has modules for different cloud providers.   
   
### Playbooks Overview   
   
   
- Multiple modules grouped together, representing one whole configuration(or all the steps) with sequential tasks with attributes such as where to execute the task(host) using which user etc is called a **Play**.   
- In a single file you can have multiple such Plays which is then called a **Playbook**.   
- Sequential modules are grouped as tasks. A task is an action to be performed. A task is composed of a module with arguments and a description describing itself.   
- To tell Ansible where to run a playbook you use the `hosts` attribute and `remote_user` attribute to inform which user is to be used to run those tasks.   
- Tasks are units of action in Ansible. You can execute a single task once with an Ad-Hoc command or multiple tasks in a playbook.   
- Playbooks are ordered lists of tasks. We can run those tasks in that order repeatedly.   
- Playbooks are written in [languages.YAML](../devlog/languages.YAML.md) and are easy to read, write, share and understand.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660994842/wiki/go7x5ljddqe6h3mifsgz.png)   
   
### Inventory Overview   
   
   
- The “hosts” defined in a Playbook is referenced in an Inventory list.   
- Inventory = all the machines involved in task executions.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1660994943/wiki/lvfbdzldmwxpovex1t7g.png)   
   
   
- It basically keeps a list of inventory, you can define (**group**) the entries in the host file as IP Addresses (they can cloud servers, virtual servers or bare metal servers) or host names.   
- Inventory is a list of managed nodes. An inventory file is also sometimes called a "host file". The inventory can specify information such as IP address, hostname or domain-name for each managed node. Default location: `/etc/ansible/hosts` (or use the `-i` flag to use a custom file). An inventory file can be formatted as an INI or [languages.YAML](../devlog/languages.YAML.md) file.   
   
## Ansible for Docker   
   
Ansible Playbook is an improved alternative to Dockerfile. You can recreate all the setup inside a Dockerfile and you can achieve the same but more.   
   
You can create a [Docker](../devlog/docker.md) Image or a [Vagrant](/not_created.md) container, deploy it to a cloud instance or a bare metal server all from a single Ansible Playbook. It helps you replicate the application across many environments. You can manage both the Docker Container and the host(storage, network) where it’s running.   
   
## Ansible Tower   
   
A UI dashboard from Red Hat.   
   
   
- Basically gives a way to centrally store all your automation tasks across teams where you can configure who can access and execute what tasks.   
- Manage inventory and get an overview of jobs, their health status.   
   
## Installation   
   
You can either install Ansible on your own local machine or on a remote machine (it may belong to a private network) and manage your nodes from that server.   
   
[Installing Ansible — Ansible Documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) Follow this documentation to install it on your machine.   
   
**Control Node**   
   
   
- The machine that runs Ansible and manages target servers.   
- Windows is not supported for control node.   
   
**Managed Node**   
   
   
- Linux servers must have Python installed.   
- Windows servers need PowerShell installed.   
- Ansible connects to target servers using SSH.   
   
## Ansible Inventory   
   
Hosts = managed servers. It stores all the IP addresses that we want to connect to. Hosts file is also called as inventory file.   
   
**Authentication**   
   
Ansible either needs username and password or private key to SSH into the severs. We can specify which private key Ansible should use for each host using the attribute `ansible_ssh_private_key_file` and to specify the username `ansible_user`   
   
```yaml
133.209.255.142 ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_user=root
```
   
   
To test connection: `ansible all -i ./hosts -m ping`   
   
**Grouping Hosts**   
   
Within hosts file we can organize our server into different groups, this will help us keep the host in order and permit us to use group variables. A host can be part of multiple groups.   
   
```ini
[droplets]
133.209.255.142 ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_user=root
134.209.255.143 ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_user=root
```
   
   
To test connection: `ansible droplets -i hosts -m ping`   
   
**Variables**   
   
Configure authentication and username for an entire group.   
   
```ini
[droplets]
133.209.255.142
134.209.255.143

[droplet:vars]
ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_user=root
```
   
   
   
---   
   
You can even use **DNS** instead of IP such as in case of configuring AWS EC2 instances with Ansible.   
   
Use `ansible_python_interpreter` to change Python interpreter.   
   
```ini
[ec2]
ec2-15-188-239-5.eu-west-3.compute.amazonaws.com
ec2-35-188-28G-I36.eu-west-3.compute.amazonaws.com ansible_python_interpreter=/usr/bin/python3
```
   
   
```ini
[servers]

vps1 ansible_host=207.154.254.221
vps2 ansible_host=167.122.186.63
vps3 ansible_host=139.59.155.232
```
   
   
   
- `ansible_host` is a predefined variable that holds the value of the managed hosts.   
- To parse the inventory file and list all the hosts defined in the inventory file:   
  - `ansible -i ./hosts --list-hosts all`   
- To check if ansible is able to communicate with the hosts   
  - `ansible -i ./hosts vps1 -m ping -u userName -k` (to test for the whole group, use the group name such as: `servers` instead of `vps1`)   
  - `-m` is for "module" in this case we're using the `ping` module - it checks the ssh authentication for the each node.   
  - `-u` defines the username that will connect to the remote hosts.   
  - `-k` to prompt for password.   
    - `sshpass` module must be installed on the controlling machine   
    - Edit `/etc/ansible/ansible.cfg` to uncomment `host_key_checking = False`   
    - If you want to test ssh communication for all the hosts in the inventory file, use option "all" instead of a group or a specific host   
- To get setup info   
  - `ansible -i ./hosts servers -m setup -u student -k`   
- To setup ssh authentication   
- You can omit the `-u` and `-k` option you can declare them in the inventory file.   
   
```ini
[servers]

vps1 ansible_host=207.154.254.221
vps2 ansible_host=167.122.186.63
vps3 ansible_host=139.59.155.232

[servers:vars]
ansible_user=student
ansible_ssh_pass=clearPW123
ansible_become_pass=sudoPWroot
ansible_port=22
```
   
   
   
- You should use a vault to securely pass your credentials instead of hardcoding it.   
- To overwrite variables for a specific host, such as using a different user to authenticate   
   
```ini
[servers]

vps1 ansible_host=207.154.254.221 ansible_user=student2
vps2 ansible_host=167.122.186.63
vps3 ansible_host=139.59.155.232

[servers:vars]
ansible_user=student
ansible_ssh_pass=clearPW123
ansible_port=22
```
   
   
**Host Key Checking**   
   
   
- It is enabled by default in Ansible.   
- It guards against server spoofing and [man-in-the-middle attack](../devlog/man-in-the-middle%20attack.md)s   
   
To automate confirmation for this check:   
   
There are two ways to handle SSH key checks   
   
   
- Authorized Keys   
- Known Hosts   
   
These are options are based on “long-lived” servers and “ephemeral” or “temporary” servers.   
   
The check should only be done once and thats it. To achieve this it has to add the known hosts to a file `~/.ssh/known_hosts` (on the control node). You can use the command `ssh-keyscan` like:   
   
`ssh-keyscan -H 165.22.201.197 >> ~/.ssh/known_hosts`   
   
Another step would be for the managed node to recognize/authenticate us. The target machine should have the control node’s public ssh key stored `~/.ssh/id_rsa.pub`. If your managed nodes are created by a server like DigitalOcean upon creating the server, it’d have added a public key to those servers by default. Which you can check under `~/.ssh/authorized_keys`.   
   
You can copy paste your public ssh key using `ssh-copy-id`.     
Like: `ssh-copy-id root@188.166.30.219` which will take the public key from the control node’s default location and copy it to the managed node’s root user.   
   
**Disable Host Key Checking**   
   
This option is viable when you’re dealing with ephemeral infrastructure(servers that are dynamically created and destroyed). It will not be a security risk as the servers are short lived anyway.   
   
Previously, an Ansible configuration file used to get created under `/etc/ansible` but in the newer version you’ve manually create one in one of the default locations:   
   
   
- `/etc/ansible/ansible.cfg`   
- `~/.ansible.cfg`   
   
```
# ~/.ansible.cfg
[defaults]
hosy_key_checking = False
```
   
   
You can also create an `ansible.cfg` for a specific project inside the project’s root dir. It is should NOT be a hidden file.   
   
   
---   
   
## Ad-Hoc Commands VS Playbooks   
   
   
- Ad-Hoc commands are not stored for future uses.   
- It is the fastest way to interact with our managed servers.   
- `ansible [pattern] -m module -a "[module options]"`   
  - `pattern` = target hosts and groups   
  - `all` = default group that contains all hosts   
- Ad-Hoc commands can be used to do quick and simple things like checking the logs, checking if a process is running, or installing a package on a list of servers.   
- Playbooks are used for big deployments, orchestration or system configuration. We use the `ansible` command to run an Ad-Hoc command and the `ansible-playbook` command to run a playbook.   
- `ansible` is used to run Ad-Hoc commands. These commands are quick and easy but are not reusable. You don't save them for later, they demonstrate the simplicity and power of ansible.   
  - Some examples are rebooting servers, updating servers, copy files, manage package, users.   
- Playbooks are scripts written in [languages.YAML](../devlog/languages.YAML.md) and are composed of one or more play in an ordered list and each play executes one or more tasks using ansible modules.   
- Both Ad-Hoc commands and Playbooks use modules to perform different tasks. Modules are units of code that do the actual work in Ansible.   
   
## Ansible Modules   
   
Ansible modules are discrete units of code which can be used from the command line or in a playbook task.   
   
The modules also referred to as task plugins or library plugins in the Ansible.   
   
Ansible ships with several modules that are called module library, which can be executed directly or remote hosts through the playbook.   
   
Users can also write their modules. These modules can control like services, system resources, files, or packages, etc. and handle executing system commands.   
   
— via [Ansible Modules - javatpoint](https://www.javatpoint.com/ansible-modules)   
   
You can find all the modules in the:   
   
   
- ~~[Module Index — Ansible Documentation](https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html)~~ (deprecated)   
- [Collection Index — Ansible Documentation](https://docs.ansible.com/ansible/latest/collections/index.html)   
   
**Examples of different modules executed directly**   
   
### The Shell Module   
   
The general syntax of running an Ad-Hoc command is:   
   
`ansible -i [path-to-invetory-file] [group-to-connect-to] -m [module] -a [module-arguments] -u [user] -k`   
`ansible -i ./hosts servers -m shell -a "df -h" -u user1 -k`   
   
By default ansible uses multi-threading, with 5 threads as the default. If you've more than 5 hosts, you can increase the threads using the `-f` option.   
   
Example:   
   
`ansible -i ./hosts servers -m shell -a "ip address show dev eth0 | grep ether | cut -d ' ' -f6 | grep -v ">>"`   
   
### The Script Module   
   
   
- This module can be used to run a local shell script on a remote system.   
- The classical method of doing something like this would be to first copy the script to the remote machines using [scp](../devlog/scp.md), connect to it and run the script.   
- Using the script module, the controlling machine's script is run on each host(in fact the local script is transferred to remote node and then executed).   
- This module is also supported for Windows targets.   
   
Example:   
   
`ansible -i ./hosts servers -m scripts -a "./backsup.sh" --become -K`   
   
`--become` to run the script as [root](../index.md) on the host machines   
`-K` to prompt for [sudo](../devlog/sudo.md) password (you can omit this if you've already declared it inside the inventory file)   
   
### The APT Module   
   
   
- This module automates software installation, removal and update.   
- It allows you to manage packages on Ubuntu(Debian) Distributions.   
- If you use other distros, use the corresponding package managers.   
   
Example:   
   
Install a specific software on all the hosts.   
   
The `state` option indicates the desired state of a package.   
   
`ansible -i ./hosts severs -m apt -a "name=nmap state=present update_cache=true" -u [user] -k --become -K`   
   
   
- Remove a specific software on all the hosts.   
   
`ansible -i ./hosts severs -m apt -a "name=nmap state=absent purge=yes update_cache=true" --become`   
   
   
- To perform a full system update on all the hosts.   
   
`ansible -i ./hosts servers -m apt "upgrade=full" --become`   
   
   
- To remove dependencies that are no longer required.   
   
`ansible -i ./hosts servers -m apt "autoremove=yes autoclean=yes" --become`   
   
### The Service Module   
   
This module is used to control the services running on the host nodes.   
   
Examples:   
   
   
- To start a service on all the hosts.   
   
`ansible -i ./hosts servers -m service -a "name=ngnix state=started" --become`   
   
   
- To reload a service on all the hosts.   
   
`ansible -i ./hosts servers -m service -a "name=ngnix state=restarted" --become`   
   
   
- To stop a service on all the hosts.   
   
`ansible -i ./hosts servers -m service -a "name=ngnix state=stopped" --become`   
   
   
- Set a service to start on boot on all the hosts.   
   
`ansible -i ./hosts servers -m service -a "name=ngnix enabled=yes" --become`   
   
### The User & Group Module   
   
   
- This module is used to manage groups, user accounts and user attributes.   
   
Examples:   
   
   
- Creating a new group on all remote hosts   
   
`ansible -i ./hosts servers -m group -a "name=developers state=present" --become`   
   
   
- Removing an existing group from all remote hosts   
   
`ansible -i ./hosts servers -m group -a "name=developers state=absent" --become`   
   
   
- Adding a new user to all remote hosts   
  - You can give comma separated values if you want to add the user to multiple groups   
  - The last three options are optional   
    `ansible -i ./hosts servers -m user -a "name=johndoe state=present groups=developers create_home=yes comment=\"new user\" shell=/bin/bash generate_ssh_key=yes ssh_key_bits=2048" --become`   
   
## Ansible Playbooks   
   
Ansible configuration files should be treated as code (Infrastructure as Code)   
   
To make a Playbook you need two files:   
   
1. Managed Nodes to target (`hosts.ini` or `hosts.yaml`)   
2. At least one task to execute (`playbook.yaml`)   
3. (OPTIONAL) `ansible.cfg`   
   
   
- **Plays and tasks run in order from top to bottom.**   
- A Playbook consists of one or multiple Plays.   
- A Play is a group of tasks.   
   
### A simple playbook   
   
```yaml
# my-playbook.yaml
--- # used to separate blocks of code
- name: configure ngnix web server
	hosts: webserver # specify an IP or a group(as referred to in the hosts file)
	tasks: # a list of commands to run for the hosts defined
		- name: install ngnix server # descriptive of what the task does
			apt:  # apt is a module here
				name: ngnix  # to install specific version of package: ngnix=1.18.0-0ubuntu1 or use regex and state: present instead of latest
				state: latest
		- name: start ngnix
			service:
				name: ngnix
				state: started
```
   
   
Without comments   
   
```yaml
---
- hosts: webserver
  name: "configure ngnix web server"
  tasks:
    - apt:
        name: ngnix
        state: latest
      name: "install ngnix server"
    - name: "start ngnix"
      service:
        name: ngnix
        state: started
```
   
   
Almost killed myself trying to validate this [languages.YAML](../devlog/languages.YAML.md).   
   
**Run a playbook**   
   
`ansible-playbook -i hosts my-playbook.yml`   
   
**Gather Facts** Module   
   
   
- Is automatically called by playbooks.   
- To gather useful variables about remote hosts that will be used in playbooks.   
- It provides all kinds of information to about the system to Ansible automatically.   
   
Ansible uses different color coding to present different kind of information kinda how Terraform does.   
   
Most Ansible modules check whether the desired state has already been achieved, they exit without performing any actions. **This is Ansible’s Idempotency**. Kinda how Terraform works.   
   
To remove Ngnix:   
   
```yaml
# my-playbook.yaml
---
- name: configure ngnix web server
  hosts: webserver
  tasks:
    - name: uninstall ngnix server
      apt:
        name: ngnix
        state: absent
    - name: stop ngnix
      service:
        name: ngnix
        state: stopped
```
   
   
## Ansible Collections   
   
In Ansible version till 2.9 and earlier had modules in them and were packed in the Ansible distributions, the code and the modules. The single package/distribution contained both the Ansible core code and the modules.   
   
From 2.10, the devs changed Ansible grew as more and more developers were contributing code/modules, they decided to separate the core Ansible from the Ansible modules and plugins.   
   
`ansible-base` contains the core Ansible programs and **Ansible Collections** contain the modules and plugins. Both of them have their own repositories and can be released independently.   
   
**Collection** VS **Module**   
   
Collection is a format for bundling and distributing Ansible all kinds of Ansible content(Playbooks, Modules, Plugins, Documentation).   
It can be released independently of the other collections.   
   
All of the modules are part of a collection. [Collection Index — Ansible Documentation](https://docs.ansible.com/ansible/latest/collections/index.html). Different modules are grouped together to form different collections.   
   
Maintenance of Modules:   
   
   
- `ansible.builtin` = ansible on Github, maintained by core team.   
- Distributed on Galaxy, maintained by community or partners.   
- Distributed on Automation Hub, maintained by content team or partners.   
   
### Ansible Galaxy   
   
   
- ansible-galaxy collection list` (this wouldn’t work on Ansible ≤ 2.9)   
- [Ansible Galaxy](https://galaxy.ansible.com/) is where the code of a collection lives.   
- It is an online hub for finding and sharing Ansible community content.   
- Kinda like [npmjs.com](https://www.npmjs.com/) or [Terraform Registry](https://registry.terraform.io/)   
- To install/update a collection `ansible-galaxy collection install amazon.aws`   
- They’re located locally under `~/.ansible/collections/`   
   
### Create Collection   
   
If you want to create a bundle/collection of yours that may or may not contain Plugins, Modules, Ansible projects/Playbooks.   
   
You’ve to follow a standard structure when creating a collection:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661013377/wiki/tvxa359uehwroa6jbs1m.png)   
   
`galaxy.html` - file contains the metadata and must be located at the root level of a collection.   
   
## Ansible Plugins   
   
   
- Pieces of code that add to Ansible’s functionality or modules. You can also write your own plugins.   
   
## Variables   
   
> Naming convention: You cannot be using reserved Python keywords as variables such as: `name`, `async` nor reserved Playbook keywords such as: `environment`.   
   
**Registered Variables**   
   
Variables that are created from the output of an Ansible task(module). This variable can be used in any later tasks in your play. Once registered it can be used in other modules such as `debug` using `{{var_name}}`, if the output is a dictionary we can access the values inside it using the dot notation `{{var_name.dictionary_item}}`   
   
```yaml
---
- name: ...
  some-module: ...
  register: var_name
- debug: msg={{var_name}}
```
   
   
**Parameterize Playbook**   
   
To parameterize a Playbook so you can set the variables from outside depending on the environment you're in.   
   
When you've a hardcoded value that may change at a later point use `{{var_name}}` variable. To not confuse Ansible with [languages.YAML](../devlog/languages.YAML.md)'s dictionary syntax when referencing a variable consider enclosing the curly braces with `""` double quotes. This is only an issue when you're using curly braces immediately after a colon `:` such as `src: "{{var_name}}"`.   
   
You can variablize only a part of a string such as: `src: /home/ghost/packages/app-1.0.0.tgz` to `src: /home/ghost/packages/app-{{version}}.tgz` and you can use multiple variables in a string(literal) such as: `src: "{{location}}/app-{{version}}.tgz"` (notice the double quotes).   
   
To set the values for the defined variables:   
   
> Set them inside your **Play**   
   
```yaml
- name: A play name
  hosts: ...
  vars:
    - location: ...
    - version: ...
```
   
   
> Set from from **outside** your Playbook   
   
You can set them during runtime(when running `ansible-playbook` commands in terminal) using the flag `--extra-vars` or `-e` and list them as key value pairs.   
   
```bash
ansible-playbook -i hosts app.yaml \
--extra-vars "version=1.0.0 location=<path>"
```
   
   
Using this way helps you keep your code [DRY](../devlog/DRY.md).   
   
**External File**   
   
When you've a large Playbook with a lot of variables, using an external file that has all the required variables can make your life easier.   
   
Create a new file named anything you'd like in the root of your Ansible code. It has to be a [languages.YAML](../devlog/languages.YAML.md) file and variables are defined in the `key: value` syntax.   
   
Reference this file in your Ansible Playbook(it can be a list of variable files). It has to be set in each play where variables are being referenced.   
   
```yaml
- name: A name for a play
  hosts: ...
  vars_file:
    - <path-to-vars-file>
```
   
   
**Variable Prompt**   
   
Playbook prompts the user for certain input. Prompting the user for variables lets you avoid recording sensitive data like passwords.   
   
```yaml
- name: A name for a play
  hosts: ...
  vars_prompt:
    - name: var_name
      prompt: Enter the variable's value
```
   
   
## Inventory Default Location   
   
Default `hosts` file location. Describe `inventory = hosts` in the `ansible.cfg` in the root of your Ansible project. You can now run `ansible-playbook app.yaml` without having to pass the hosts file.   
   
## Dynamic Inventory   
   
Let's say we're managing an inventory which fluctuates over time, the hosts spinning up and shutting down all the time. Maybe auto-scaling is at play, in such a case having a static list of IP address in our inventory file doesn't make sense, because ephemeral servers are assigned different IP addresses. We need a way to **dynamically** set DNS names or IP addresses.   
   
   
**Overview**   
   
   
- Let's create 3 EC2 instances with [terraform](../devlog/terraform.md)   
- Connect to these servers with Ansible without hardcoding the IP address.   
   
**Inventory Plugin vs Inventory Script**   
   
In our Ansible code we need the functionality to connect to our AWS account, fetch server information. For this we've dynamic inventory scripts and plugins. Ansible recommends using plugins over scripts. Because plugins can use the state management of Ansible. Plugins are written in [languages.YAML](../devlog/languages.YAML.md). Scripts are written in Python.   
   
   
- There are different plugins/scripts for different infrastructure provider.   
- `ansible-doc -t inventory -l` to list all available plugins.   
- We'll use the AWS plugin in our case.   
   
**`aws_ec2` Plugin**   
   
   
- The prerequisites of using the plugin is that you need [boto](../devlog/boto.md)3 and `botocore` installed on your local machine.   
- Enable the plugin inside `ansible.cfg` like `enable_plugins = aws_ec2`.   
- Create a config file named `inventory_aws_ec2.yaml`, `.yaml`is required.   
   
```yaml
# inventory_aws_ec2.yaml
---
plugin: aws_ec2
regions:
  # get all hosts from specific region(s)
  - eu-west-3
```
   
   
   
- `ansible-inventory` to display or dump the configured inventory as Ansible sees it.   
  - `ansible-inventory -i inventory_aws_ec2.yaml --list`   
  - `ansible-inventory -i inventory_aws_ec2.yaml --graph`   
   
**Assign public DNS to EC2 instances**   
   
The `ansible-inventory ...` command will return a list **private** DNS names. We cannot use these to connect to them. We need to assign them **public** DNS names if we want to interact with it from outside the VPC(where the servers live).   
   
In the [Terraform](../devlog/terraform.md) code:   
   
```t
resource "aws_vpc" "myapp-vpc" {
  cidr_block = var.vpc_cidr_block
  enable_dns_hostnames = true
  tags = {
      Name = "${var.env_prefix}-vpc"
  }
}
```
   
   
**Configure Ansible to use dynamic inventory**   
   
In the Ansible code, set the `hosts:` to either `all` or `aws_ec2`. You also need private key and user. Like:   
   
```cfg
remote_user = ec2-user
private_key_file=~/.ssh/id_rsa
```
   
   
Run the playbook:   
   
`ansible-playbook -i inventory_aws_ec2.yaml deploy-app.yaml`   
   
You can also make the `inventory_aws_ec2.yaml` as the default host file inside the `ansible.cfg` file. Like: `inventory = inventory_aws_ec2.yaml`.   
   
**Target only specific servers**   
   
What if you wanted to target only specific servers. In the plugin configuration, you can use `filters` to filter the servers you want to use. The same filter attributes that are used by [aws.cli](../devlog/aws.cli.md). In our case, let's use the tag name.   
   
```yaml
filters:
  tag:Name: dev*
  instance-state-name: running
```
   
   
**Create dynamic groups**   
   
You can group different servers in the plugin configuration file.   
   
Example: grouped by tag.   
   
```yaml
---
plugin: aws_ec2
regions:
  - eu-west-3
keyed_groups:
  - key: tags
    prefix: "tag"
  # the values/attributes used here are from the output of `ansible-inventory ...` not the same attributes as `filters`
```
   
   
You can select the tag name and use it as the `hosts:` value in the Ansible code.   
   
Example: group by instance type   
   
```yaml
---
plugin: aws_ec2
regions:
  - eu-west-3
keyed_groups:
  - key: tags
    prefix: "tag"
  - key: instance_type
    prefix: instance_type
```

   
   
   
You can use roles when your Ansible code is too complex, with a lot of tests stuff. You can group your content into roles. It can help you break your large Playbooks into smaller manageable files. To easily reuse and share them with others.   
   
Think of roles like functions in a programming language: It lets you extract some logic and use it elsewhere with different parameters/arguments.   
   
Roles are like:   
   
   
- Like a package for your tasks in your playbooks.   
- You can extract tasks from playbooks.   
- Re-use roles in different plays.   
- Results in much cleaner plays.   
- Allows you to develop and test separately.   
- You can use existing roles from community.   
  - You can find these roles on Galaxy or public Git repos.   
   
A role can have the following stuff:   
   
   
- Tasks that the role executes.   
- Static files that the role deploys.   
- (Default) variables for the tasks, to parameterize role with the possibility of overwriting the defaults.   
- Custom modules, which are used within the role.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661521705/wiki/dlzswizbnsm3tlm8liic.png)   
   
Roles also(like collections) have a predefined structure:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661521825/wiki/cjflpavfd8qiwnihca5a.png)   
   
**Create a role**   
   
   
- Let's refactor [deploy-docker-new-user.yml](https://gitlab.com/zubayrrr/ansible-learn/-/blob/master/deploy-docker-new-user.yaml) with roles.   
- Create a dir named "roles" in the root of your Ansible code.   
- Create folders named `create_user` and `start_containers`.   
  - In each dir create "tasks" dir.   
  - Create `main.yml` in each of those tasks folders.   
- Extract the code from your playbook which you want to be a role and paste it inside it's corresponding `/tasks/main.yml`. Make sure you fix the indentation.   
   
**Using roles in plays**   
   
To reference the roles inside the playbook: instead of defining `tasks`, you simply use `roles` and list the roles you want to execute in that play.   
   
```yaml
---
- name: Install python3, docker, docker-compose
  hosts: all
  become: yes
  gather_facts: False
  tasks:
    - name: Install python3 and docker
      vars:
        ansible_python_interpreter: /usr/bin/python
      ansible.builtin.yum:
        name:
          - python3
          - docker
        update_cache: yes
        state: present
    - name: Install Docker-compose
      ansible.builtin.get_url:
        url: https://github.com/docker/compose/releases/download/1.27.4/docker-compose-Linux-{{lookup('pipe', 'uname -m')}}
        dest: /usr/local/bin/docker-compose
        mode: +x
    - name: Start docker daemon
      ansible.builtin.systemd:
        name: docker
        state: started
    - name: Install docker python module
      ansible.builtin.pip:
        name:
          - docker
          - docker-compose

- name: Create new linux user
  hosts: all
  become: yes
  vars:
    user_groups: adm,docker
  roles:
    - create_user

- name: Start docker containers
  hosts: all
  become: yes
  become_user: nana
  vars_files:
    - project-vars
  roles:
    - start_containers
```
   
   
You can package much more than just tasks inside a role. Like static files, we can package them inside a role as well. It is a common practice to use this feature for passing scripts, configuration files.   
   
For example: create a `roles/start_containers/files/` dir and create `docker-compose.yaml` file inside it and now you can reference the file as:   
   
```yaml
# roles/start_container/tasks/main.yml
---
- name: Copy docker compose
  ansible.builtin.copy:
    src: docker-compose.yaml
    dest: /home/nana/docker-compose.yaml

- name: Docker login
  community.docker.docker_login:
    registry_url: "{{ docker_registry }}"
    username: "{{ docker_username }}"
    password: "{{ docker_password }}"

- name: Start container from compose
  community.docker.docker_compose:
    project_src: /home/nana
```
   
   
**Variables in roles**   
   
You can define variables inside roles as well and assign values to them in the `/roles/role_name/vars/main.yml`   
   
```yaml
# /roles/start_container/vars/main.yml
docker_registry: https://index.docker.io/v1/
docker_username: nanajanashia
```
   
   
To overwrite these variables check the variable precedence.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1661524594/wiki/w4bqujfeifzonbkqvofh.png)   
   
If you want to define default variables you can do so in the `/role/role_name/defaults/main.yml` the users if they want to overwrite the variables in `../vars` folder or as command line args as they’ve lower precedence.   
   
You can find the finish code at [zubayrrr / ansible-learn · GitLab](https://gitlab.com/zubayrrr/ansible-learn/-/tree/master/)
   
   
## Labs   
   
   
- [ansible.deploy nodejs application](../devlog/ansible.deploy%20nodejs%20application.md)   
- [ansible.Deploy Nexus](../devlog/ansible.Deploy%20Nexus.md)   
- [ansible.Run Docker Applications](../devlog/ansible.Run%20Docker%20Applications.md)   
- [ansible.integrate ansible with terraform](../devlog/ansible.integrate%20ansible%20with%20terraform.md)   
- [ansible.Deploying Application in K8s](../devlog/ansible.Deploying%20Application%20in%20K8s.md)   
- [ansible.Run Ansible from Jenkins Pipeline](../devlog/ansible.Run%20Ansible%20from%20Jenkins%20Pipeline.md)   
   
## Misc   
   
   
- [Return Values — Ansible Documentation](https://docs.ansible.com/ansible/latest/reference_appendices/common_return_values.html)   
- `ansible-playbook app.yaml -vv` returns metadata information about the Playbook and the modules used in it.   
   
## Resources   
   
   
- [geerlingguy/ansible-for-devops: Ansible for DevOps examples.](https://github.com/geerlingguy/ansible-for-devops)   
   
## Look into   
   
   
- post tasks   
- pre tasks