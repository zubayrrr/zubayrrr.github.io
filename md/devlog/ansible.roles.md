---
created: 1661522088401
desc: ''
id: 9e28wxzup8gc8tb2fgmqx9w
title: Roles
updated: 1661524533507
---
   
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