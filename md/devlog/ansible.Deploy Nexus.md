---
created: 1661174387857
desc: ''
id: pfsx41kw55v89mleiawdhza
title: Deploy Nexus
updated: 1661210032090
---
   
**Automate Installing** & **Starting [Nexus](../devlog/nexus.md) on a Remote Server** using [ansible](../devlog/ansible.md)   
   
Steps:   
   
1. Create a Droplet   
2. Write Ansible Playbook   
   a. Download Nexus binary and unpack   
   b. Run Nexus application using Nexus user   
   
   
---   
   
   
- Create a `hosts` file   
   
```ini
<ip-address> ansible_ssh_private_key=~/.ssh/id_rsa ansible_user=root
```
   
   
   
- Create a `deploy-nexus.yml` Playbook   
   
```yaml
- name: Update repo & install java and net-tools
  hosts: <ip-address>
  tasks:
    - name: Update apt repo and cache
      apt: update_cache=yes force_apt_get=yes cache_valid_time=300
    - name: Install Java 8
      apt: name=openjdk-8-jre-headless
    - name: Install net-tools
      apt: name=net-tools

- name: Download Nexus and unpack it
  hosts: <ip-address>
  tasks:
    - name: check if nexus folder stats
      stat:
        path: /opt/nexus
      register: stat_result
    - debug: msg={{stat_result.stat.exists}}
    - name: Download Nexus
      # download files from https, http or FTP to the remote server, use win_get_url for Windows
      get_url:
        url: https://download.sonatype.com/nexus/3/latest-unix.tar.gz
        dest: /opt/
      register: downloaded
    - debug: msg={{downloaded}}
    - name: Untar Nexus installer
      unarchive:
        src: "{{downloaded.dest}}"
        dest: /opt/
        remote_src: yes
      when: not stat_result.stat.exists
    - name: Find nexus folder name # step to demonstrate find module
      find:
        paths: /opt/
        pattern: "nexus-*" # regex
        file_type: directory
      register: find_result
    - debug: msg={{find_result}}
    - name: Rename Nexus folder
      shell: mv {{find_result.files[0].path}} /opt/nexus # beware of shell module's non idempotency
      when: not stat_result.stat.exists

- name: Create nexus user to own nexus folders
  hosts: <ip-address>
  tasks:
    - name: Ensure group exists/create
      group: # use win_group for Windows
        name: nexus
        state: present
    - name: Create nexus user
      user: # use win_user for Windows
        name: nexus
        state: present
    - name: Make nexus user own of nexus folder recursively
      file:
        path: /opt/nexus
        state: directory
        owner: nexus
        group: nexus
        recursive: yes
    - name: Make nexus user own of sonatype-work folder recursively
      file:
        path: /opt/sonatype-work
        state: directory
        owner: nexus
        group: nexus
        recurse: yes

- name: Start nexus with nexus uer
  hosts: <ip-address>
  become: true
  become_user: nexus
  tasks:
    - name: Set run_as_user nexus
      # blockinfile - insert/update/remove multi-line text surrounded by customizable marker lines
      # blockinfile:
      #   path: /opt/nexus/bin/nexus.rc
      #   block: | # this is yaml syntax rep multiline string
      #     run_as_user="nexus"
      # lineinfile module ensure/replace existing line using regex, useful when changing a single line, see "replace" module to change multiple lines
      lineinfile:
        path: /opt/nexus/bin/nexus.rc
        regexp: '^#run_as_user=""'
        line: run_as_user="nexus"
    - name: Start nexus
      command: /opt/nexus/bin/nexus start

- name: Verify nexus is running
  hosts: <ip-address>
  tasks:
    - name: Check with ps
      shell: ps aux | grep nexus
      register: app_status
    - debug: msg={{app_status.stdout_lines}}
    - name: Wait for one minute
      pause:
        minutes: 1
    - name: Check with netstat
      shell: netstat -plnt
      register: app_status
    - debug: msg={{app_status.stdout_lines}}
```
