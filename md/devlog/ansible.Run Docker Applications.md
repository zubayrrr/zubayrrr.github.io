---
created: 1661247786484
desc: ''
id: 60tz21wxjaoe6u8vsslkuzp
title: Run Docker Applications
updated: 1661337898856
---
   
Steps:   
   
1. [terraform.Automate Provisioning EC2](/not_created.md) (with TF)   
2. Configure inventory file to connect to instance   
3. Write Ansible Playbook   
   a. Install [Docker](../devlog/docker.md) and `docker-compose`   
   b. Copy `docker-compose` file to server   
   c. Start Docker containers to run application   
   
   
---   
   
## Create AWS EC2 instance with [Terraform](../devlog/terraform.md)   
   
We'll achieve instantiating of EC2 instance using Terraform, except for the `user_data`, which'll install Docker and configure it, we're going to have Ansible do that part of the setup.   
   

   
In this lab, we'll do:   
   
   
- Provision an [aws.EC2](../devlog/aws.EC2.md) instance on AWS.   
- Run a simple [nginx](../devlog/nginx.md) [docker](../devlog/docker.md) container on it.   
- We'll do this on AWS infrastructure using Terraform (obviously).   
   
## Steps   
   
1. Create custom VPC   
2. Create custom Subnet   
3. Create Route table and Internet Gateway.   
   
   - To connect the VPC to the internet.   
   - Allow traffic to and from VPC.   
4. Deploy EC2 instance on the Subnet.   
5. Deploy ngnix Docker container.   
6. Create Security Group(Firewall), opening ports.   
   
   - In order to access the Web Application.   
   - And also to SSH into that EC2 server.   
   
## Create VPC and Subnet   
   
```terraform
provider "aws" {
  region = "eu-central-1"
}

variable vpc_cidr_block {}
variable subnet_1_cidr_block {}
variable avail_zone {}
variable env_prefix {}
variable instance_type {}
variable ssh_key {}
variable my_ip {}

data "aws_ami" "amazon-linux-image" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }
}

output "ami_id" {
  value = data.aws_ami.amazon-linux-image.id
}

resource "aws_vpc" "myapp-vpc" {
  cidr_block = var.vpc_cidr_block
  tags = {
      Name = "${var.env_prefix}-vpc"
  }

  # Route table is auto-generated for your VPC by AWS
  # Default Network ACL - firewall configuration (applied to subnet in that VPC)
}

resource "aws_subnet" "myapp-subnet-1" {
  vpc_id = aws_vpc.myapp-vpc.id
  cidr_block = var.subnet_1_cidr_block
  availability_zone = var.avail_zone
  tags = {
      Name = "${var.env_prefix}-subnet-1"
  }
}

resource "aws_security_group" "myapp-sg" {
# BTW you can also just use the default SG that was generated when VPC was created
# resource "aws_default_security_group" "default-sg" { # you really only need to change this, rest remains the same
  name   = "myapp-sg"
  vpc_id = aws_vpc.myapp-vpc.id

# Defining traffic rules for firewall
  ingress {
    from_port   = 22
    to_port     = 22 # you can even set a range of ports but we only need 22
    protocol    = "tcp"
    cidr_blocks = [var.my_ip]
  }

  ingress {
    from_port   = 8080
    to_port     = 8080
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    # allow any traffic to leave server
    from_port       = 0
    to_port         = 0
    protocol        = "-1" # any protocols
    cidr_blocks     = ["0.0.0.0/0"]
    prefix_list_ids = []
  }

  tags = {
    Name = "${var.env_prefix}-sg"
  }
}

resource "aws_internet_gateway" "myapp-igw" {
	vpc_id = aws_vpc.myapp-vpc.id

    # Think of it as a virtual modem
    # Even though it has to be created before Route table, you don't necessarily have to put this block before the route table block.
    # Terraform knows in which sequence it needs to create components.
    tags = {
     Name = "${var.env_prefix}-internet-gateway"
   }
}

resource "aws_route_table" "myapp-route-table" {
   vpc_id = aws_vpc.myapp-vpc.id

    # Think of it as a virtual router inside your VPC
    # Create a new Route table as it is a best practice(not going with the default that comes with VPC creation)
    # default route, mapping VPC CIDR block to "local", created implicitly and cannot be specified.
   route {
     cidr_block = "0.0.0.0/0"
     gateway_id = aws_internet_gateway.myapp-igw.id
   }

   # Route table basically routes traffic within your VPC  (local)
   # You have to add an Internet Gateway to connect your VPC to the internet
   # Check "routes" in your Route Table for 0.0.0.0/0 (destination) and there has to be an Internet Gateway(as target)

   tags = {
     Name = "${var.env_prefix}-route-table"
   }
 }

# Associate subnet with Route Table
# All the resource that will be deployed in the subnet, all the traffic will be handled by the route table once the association has been made.
resource "aws_route_table_association" "a-rtb-subnet" {
  subnet_id      = aws_subnet.myapp-subnet-1.id
  route_table_id = aws_route_table.myapp-route-table.id
}

# To use the default route table instead of creating a new one

# resource "aws_default_route_table" "main-rtb" {
#   # get default route table id by terraform state show aws_vpc.myapp-vpc(it has to exist) to list all attribute it has
#   default_route_table_id = aws_vpc.myapp-vpc.default_route_table_id
#   route {
#      cidr_block = "0.0.0.0/0"
#      gateway_id = aws_internet_gateway.myapp-igw.id
#    }

#   tags = {
#      Name = "${var.env_prefix}-main-rtb"
#    }

# In this case, you don't need to add subnet association as "main" route tables as default subnet gets auto-assigned
# }


# automated key generation
resource "aws_key_pair" "ssh-key" {
  key_name   = "myapp-key"
  # public_key = var.my_public_key
  public_key = file(var.ssh_key) # this should exist locally - you should create it yourself.
}

output "server-ip" {
    value = aws_instance.myapp-server.public_ip
}

resource "aws_instance" "myapp-server" {
  # required
  ami                         = data.aws_ami.amazon-linux-image.id
  instance_type               = var.instance_type

  # create a public-private key sshing into the EC2 instance, don't forget to `chmod 400 ~/.ssh/.pem` after moving it to `~/.ssh` - this applies only when you manually create it

  key_name                    = "myapp-key"

  # optional
  associate_public_ip_address = true
  subnet_id                   = aws_subnet.myapp-subnet-1.id
  vpc_security_group_ids      = [aws_security_group.myapp-sg.id]
  availability_zone			      = var.avail_zone

  tags = {
    Name = "${var.env_prefix}-server"
  }

  user_data = <<EOF
                 #!/bin/bash
                 apt-get update && apt-get install -y docker-ce
                 systemctl start docker
                 usermod -aG docker ec2-user
                 docker run -p 8080:8080 nginx
              EOF
}

resource "aws_instance" "myapp-server-two" {
  ami                         = data.aws_ami.amazon-linux-image.id
  instance_type               = var.instance_type
  key_name                    = "myapp-key"
  associate_public_ip_address = true
  subnet_id                   = aws_subnet.myapp-subnet-1.id
  vpc_security_group_ids      = [aws_security_group.myapp-sg.id]
  availability_zone			      = var.avail_zone

  tags = {
    Name = "${var.env_prefix}-server-two"
  }

  # you can refer a bash file instead of writing it here

  # doing the below changes will cause your EC2 instance to replaced(destroy and create)
  # user_data = file("entry-script.sh") # this file has to be located in your terraform dir
  # Ideally, Terraform should only be used for initial infra setup/management, but for setting up applications and servers, you should probably use something like Ansible or Chef.
  user_data = <<EOF
                 #!/bin/bash
                 apt-get update && apt-get install -y docker-ce
                 systemctl start docker
                 usermod -aG docker ec2-user
                 docker run -p 8080:8080 nginx
              EOF
}
```
   
   
You can find the cleaner version of this on [main.tf · feature/deploy-to-ec2 · zubayrrr · GitLab](https://gitlab.com/zubayrrr/terraform-learn/-/blob/feature/deploy-to-ec2/main.tf)
   
   
Copy the IP Address to be used in the Ansible inventory(hosts) file.   
   
## Configuring Docker using Ansible   
   
**Setting up the inventory file**   
   
```ini
[docker_server]
<ec2-ip-address> ansible_ssh_private_key=~/.ssh/id_rsa ansible_user=ec2-user

interpreter_python = /usr/bin/python3
```
   
   
**Writing the Ansible Playbook**   
   
Create a new file `deploy-docker.yml`   
   
```yaml
- name: Install Python 3 and Docker and docker-compose and start docker
  hosts: docker_server
  become: yes # become_user: root - this value is set by default when become: yes is set
  gather_facts: False
  tasks:
    - name: ensure python3 and docker is installed
      vars:
        ansible_python_interpreter: /usr/bin/python
      yum: # yum only works with python2
        name:
          - python3
          - docker
        update_cache: yes
        state: present
    - name: Download docker-compose and install # on ec2 docker-compose cannot be installed using yum
      get_url:
        url: https://github.com/docker/compose/releases/download/v2.10.0/docker-compose-linux-{{lookup('pipe', 'uname -m)}}
        # lookup plugins are Ansible-specific extensions of Jinja2 templating language, they allow Ansible to get data from outside sources.
        # 'pipe' is an Ansible lookup plugin, it calculates the output of the shell command and pipes it to the left side of your lookup
        dest: /usr/local/bin/docker-compose
        mode: +x # execute
    - name: ensure docker daemon is running
      systemd:
        name: docker
        state: started
    - name: install docker python module
      pip:
        name:
          - docker
          - docker-compose

- name: Add ec2_user to docker group
  hosts: docker_server
  become: yes
  tasks:
    - name: add ec2_user to docker group
      user:
        name: ec2_user
        groups: docker
        append: yes # this only takes affect after session restart
    - name: reconnect to server session
      meta: rest_connection
# - name: test docker pull
#   hosts: docker_server
#   tasks:
#     - name: pull redis
#       command: docker pull redis

# use community.docker collection's docker* modules instead of using command module

# FQCN = fully qualified collection name should be named when referencing a community module

# - name: test docker pull
#   hosts: docker_server
#   tasks:
#     - name: pull redis
#       docker_image:
#         name: redis
#         source: pull

- name: Start docker containers
  hosts: docker_server
  vars_prompt:
    - name: docker_password
      prompt: Enter password for Docker registry
  tasks:
    - name: ensure the docker-compose file is copied from control node to managed node
      copy:
        src: <path-to-docker-compose.yaml>
        dest: /home/ec2-user/docker-compose.yaml
    - name: Docker login
      docker_login:
        registry_url: https://index.docker.io/v1
        username: <docker-id>
        password: "{{password}}"
        # if successful will generate a `~/.docker/config.json`
    - name: Start containers from docker-compose
      docker_compose:
        project_src: /home/ec2-user
        state: present # default
```
   
   
## Making the Playbook more general purpose   
   
Currently, this Playbook would only work on EC2 instances and distros that use yum. Let's change that and make it more generic.   
   
```yaml
- name: Install Python 3 and Docker and docker-compose and start docker
  hosts: docker_server
  become: yes
  gather_facts: False
  tasks:
    - name: ensure python3 and docker is installed
      vars:
        ansible_python_interpreter: /usr/bin/python
      yum:
        name:
          - python3
          - docker
        update_cache: yes
        state: present
    - name: Download docker-compose and install
      get_url:
        url: https://github.com/docker/compose/releases/download/v2.10.0/docker-compose-linux-{{lookup('pipe', 'uname -m)}}

        dest: /usr/local/bin/docker-compose
        mode: +x
    - name: ensure docker daemon is running
      systemd:
        name: docker
        state: started
    - name: install docker python module
      pip:
        name:
          - docker
          - docker-compose

- name: Create new linux user
  hosts: docker_server
  become: yes
  tasks:
    - name: Create new Linux user
      user:
        name: ghost
        groups: "{{user_groups}}" # adm,docker

- name: Start docker containers
  hosts: docker_server
  become: yes
  become_user: ghost
  vars_prompt:
    - name: docker_password
      prompt: Enter password for Docker registry
  tasks:
    - name: ensure the docker-compose file is copied from control node to managed node
      copy:
        src: <path-to-docker-compose.yaml>
        dest: /home/ghost/docker-compose.yaml
    - name: Docker login
      docker_login:
        registry_url: https://index.docker.io/v1
        username: <docker-id>
        password: "{{password}}"
    - name: Start containers from docker-compose
      docker_compose:
        project_src: /home/ghost
        state: present
```
