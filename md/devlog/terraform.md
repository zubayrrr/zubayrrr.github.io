---
created: 1653430082985
desc: ''
id: mkwoo3ek4y6bnddpy1iteb9
title: Terraform
updated: 1661538846040
---
   
> [!info]   
> [Terraform](https://www.terraform.io/intro): "HashiCorp Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share. You can then use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle. Terraform can manage low-level components like compute, storage, and networking resources, as well as high-level components like DNS entries and SaaS features."   
   
Terraform is an open source infrastructure as code ([IaC](../devlog/IaC.md)) software tool that allows DevOps engineers to programmatically provision the physical resources an application requires to run. To create and configure infrastructure NOT for installing stuff on the server, just for provisioning.   
   
It is a universal [IaC](../devlog/IaC.md) tool, works with different cloud providers and technologies.   
   

   
Infrastructure as code is an IT practice that manages an application's underlying IT infrastructure through programming. This approach to resource allocation allows developers to logically manage, monitor and provision resources -- as opposed to requiring that an operations team manually configure each required resource.   
   
Managing infrastructure (servers, network, etc) through definition files rather than manual configuration. Much like [configuration management](../devlog/configuration%20management.md), this enables automation, consistency, and is self-documenting.
   
   
## Features   
   
It uses declarative syntax(as opposed to imperative syntax) to define what the end result looks like and it will figure out how to provision the infrastructure.   
   
   
- It is also helps in automating the infrastructure as it changes over time.   
- To replicate the same infrastructure in different environments(Dev, Staging, Production)   
   
Using Terraform, your infrastructure is idempotent. You don't need to remember the current state, you only define your desired state. Since, you use declarative syntax, you don't define the steps like you would if you were using imperative syntax.   
   
## HCL   
   
It uses a DSL(domain-specific language) called "HCL" (Hashicorp Configuration Language). A declarative language for defining infrastructure.   
   
## Typical Terraform Workflow   
   
1.  Write Terraform definitions: `.tf` files written in HCL that described the desired infrastructure state (and run `terraform init` at the very beginning)   
2.  Review: With command such as `terraform plan` you can get a glance at what Terraform will perform with the written definitions   
3.  Apply definitions: With the command `terraform apply` Terraform will apply the given definitions, by adding, modifying or removing the resources   
   
This is a manual process. Most of the time this is automated so user submits a PR/MR to propose Terraform changes, there is a process to test these changes and once merged they are applied (`terraform apply`).   
   
## Automated Terraform Workflow   
   
> [!summary]    
> [Automation of Terraform can come in various forms, and to varying degrees. Some teams continue to run Terraform locally but use wrapper scripts to prepare a consistent working directory for Terraform to run in, while other teams run Terraform entirely within an orchestration tool such as Jenkins.](https://developer.hashicorp.com/terraform/tutorials/automation/automate-terraform)   
   
There are several ways to automate Terraform workflows, depending on your specific needs and environment. Here are a few common approaches:   
   
1.  Use a continuous integration (CI) tool such as Jenkins, CircleCI, or TravisCI to automate the process of running Terraform commands. This allows you to define a set of tasks that are run automatically whenever certain events occur, such as code changes or new deployments.   
2.  Use a cloud-based automation service such as AWS CodePipeline or Azure DevOps to manage your Terraform workflows. These services provide a web-based interface for defining and executing Terraform tasks, and can integrate with other tools such as GitHub or AWS S3.   
3.  Write custom scripts or programs to automate your Terraform workflows. This approach allows you to define your own logic for running Terraform tasks and integrating with other tools or services.   
   
## [ansible](../devlog/ansible.md) VS Terraform   
   
   
- Terraform is mainly an infrastructure provisioning tool.   
- Ansible is mainly used for configuring infrastructure.   
- Its a common practice to combine both to get the best of both.   
   
[To be clear, CM tools can be used to provision resources so in the end goal of having infrastructure, both Terraform and something like Ansible, can achieve the same result. The difference is in the how. Ansible doesn't saves the state of resources, it doesn't know how many instances there are in your environment as opposed to Terraform. At the same time while Terraform can perform configuration management tasks, it has less modules support for that specific goal and it doesn't track the task execution state as Ansible. The differences are there and it's most of the time recommended to mix the technologies, so Terraform used for managing infrastructure and CM technologies used for configuration on top of that infrastructure.](https://github.com/bregman-arie/devops-exercises/tree/master/topics/terraform#exercises)   
   
## Terraform Architecture   
   
It has 2 components:   
   
### Core   
   
   
- Takes 2 input sources   
	- Terraform Config   
	- State(current state of the infrastructure)   
- Core takes the input from the config and state and compares what needs to be changed and what is already there as per the config and state.   
- It essentially **creates the execution plan** that the providers use.   
   
### Providers   
   
   
- This can be providers for the specific technology(AWS, GCP, Azure, OpenStack, other [IaaS](../devlog/IaaS.md))   
- It can also has providers for higher level technologies([kubernetes](../devlog/kubernetes.md), other [PaaS](/not_created.md) or even [SaaS](/not_created.md))   
- It has over 100 providers and over 1000 resources.   
- `terraform init` will automatically recognize what providers are being used and it’ll initialize them for you.   
   
## Example config files   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655346903/wiki/lazrvzt8omhhkplp3xwt.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655346973/wiki/tcxkbpv4dyrx9yjtnufu.png)   
   
We only define a few attributes in the configuration file, the rest or defaults are handled by Terraform. Auto-generated.   
   
## Terraform commands for different stages   
   
   
- `refresh` - query infra provider to get current state.   
- `plan` - create an execution plan, just preview no real changes.   
- `apply` - executes the plan(it does all the above steps, like refresh and plan and then apply).   
- `destroy` - destroys the resources/infrastructure in the right order, does cleaning up of the resources. Reverting. It works similar to `apply`, it checks the state and makes a plan for what needs to be done.   
   
## Providers   
   
   
- They're basically a piece of code that knows how to talk to a specific technology. To connect to it and start using. Interact.   
- Expose resources for specific technology(AWS, GCP, Azure, OpenStack, other [IaaS](../devlog/IaaS.md))   
- Responsible for understanding API of that platform.   
- [Browse Providers | Terraform Registry](https://registry.terraform.io/browse/providers)   
- Providers don't come with installation of Terraform, they need to be installed separately.   
- Once provider is installed using the `terraform init` command, the complete API of that provider is available.   
- You get 2 components from the Providers   
	- Resources   
	- Data Sources   
- [Install a Terraform Provider](../devlog/Install%20a%20Terraform%20Provider.md)   
- [Terraform AWS Provider](../devlog/Terraform%20AWS%20Provider.md)   
   
## Resources   
   
   
- You can use the `resource` keyword in your `.tf` file using the resource's name.   
- The name of a resource follows the convention of `<provider>_<resource>`.   
- You can assign the resource to a variable by providing a variable name right after the resource name.   
- Each resource block describes one or more infrastructure objects. As referred to as "attributes" or "parameters".   
- When you're creating a resource for another resource that doesn't yet exist, you can reference the object.   
   
## Data Sources   
   
   
- Allows data to be fetched for use in the `.tf` files.   
- Query existing resources/components.   
- It follows the same convention as the resource names.   
   
## Terraform Commands   
   
   
- `terraform init` - initialize the working directory. Installs the providers defined in the config file.   
- `terraform apply` - apply the changes using the configuration file in the working directory.   
- `terraform apply -auto-approve` - to skip the approve prompt.   
- `terraform destroy` - if `-target` is not specified, it'll destroy all of the resources defined in the configuration file.   
   
## Examples   
   
### Creating an EC2 instance with Terraform   
   
```json
provider "aws" {
  region = "us-east-1"
  access_key = "AKIAJX7X7X7X7X7X7X7X"
  secret_key = "secret"
  // don't hard code the above values use Environment variables
}

resource "aws_vpc" "test_vpc" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "test-subnet-1" {
  vpc_id = aws_vpc.test_vpc.id
  cidr_block = "10.0.10.0/24"
  availability_zone = "us-east-1a"
}

// if you wanted to create a subnet for an existing vpc, you could hard code the ID of your vpc OR use data sources

data "aws_vpc" "existing_vpc" {
  //  use filter or attributes to filter through of your existing vpc/resource
  default = true
}

resource "aws_subnet" "test-subnet-2" {
  vpc_id = data.existing_vpc.id
  cidr_block = "172.31.48.0/20"
  availability_zone = "us-east-1a"
```
   
   
### Changing resources   
   
Adding names using `tags:` keyword and using the reserved `Name` attribute for defining a name.   
To remove something, you'd simply remove it from the config file.   
   
```json
provider "aws" {
  region = "us-east-1"
  access_key = "AKIAJX7X7X7X7X7X7X7X"
  secret_key = "secret"
  // don't hard code the above values
}

resource "aws_vpc" "test_vpc" {
  cidr_block = "10.0.0.0/16"
  tags = {
    Name: "development-vpc",
    vpc_env: "dev"
  }
}

resource "aws_subnet" "test-subnet-1" {
  vpc_id = aws_vpc.test_vpc.id
  cidr_block = "10.0.10.0/24"
  availability_zone = "us-east-1a"
    tags = {
    Name: "development-subnet"
  }
}

// if you wanted to create a subnet for an existing vpc, you could hard code the ID of your vpc OR use data sources

data "aws_vpc" "existing_vpc" {
  //  use filter or attributes to filter through of your existing vpc/resource
  default = true
}

resource "aws_subnet" "test-subnet-2" {
  vpc_id = data.existing_vpc.id
  cidr_block = "172.31.48.0/20"
  availability_zone = "us-east-1a"
```
   
   
### Removing/Destroying resources   
   
1. Remove the resource from Terraform config file and `terraform apply`. (Recommended)   
2. `terraform destroy -target resource_type.resource_name`   
   
## State   
   
`terraform.tfstate` - it is a `json` file where Terraform stores the state of your managed infrastructure. It generates this file on your first `terraform apply`.   
   
`terraform.tfstate.backup` is the file that is created to store the backup of the previous state.   
   
Neither of these files should be updated manually and must be updated as a result of executing `terraform` commands.   
   
Terraform has commands to access the information in the state file.   
   
   
- `terraform state` - list all subcommands of `state`.   
- `terraform state list` - list all resources in the state.   
- `terraform state mv` - move an item in the state.   
- `terraform state show` - show a resource in the state. Useful for checking the values of the attributes that were autogenerated by Terraform.   
   
## Output   
   
We can define what value we want Terraform to spit at the end of applying of the configuration from the resources. Output values are like function's return values.   
   
```json
output "dev-vpc-id" {
  value = aws_vpc.development_vpc.id
}

output "dev-subnet-id" {
  value = aws_subnet.dev-subnet-1.id
}
```
   
   
## Variables   
   
You use variables inside of the configuration file. variables = input variables. If you don't want to hard code values you can pass them as parameters. Define and reference it. Input variables are like function arguments. They're defined using `variable` keyword. Makes it easier to replicate, parameterize, and reuse the same configuration over different environments. You'd have different `.tfvars` files for different environments.   
   
```json
variable "subnet_cidr_block" {
  description = "CIDR block for the subnet"
  default = "10.0.30.0/24"
  type = string
}

resource "aws_vpc" "development_vpc" {
  vpc_id = aws_vpc.test_vpc.id
  cidr_block = var.subnet_cidr_block
  availability_zone = "us-east-1a"
  tags: {
    Name: "subnet-1-dev"
  }
}
```
   
   
There are three ways to pass values to input variables.   
   
1. Prompt when `terraform apply` is run.   
2. Define the value when running apply command   
   
   - `terraform apply -var "subnet_cidr_block=10.0.30.0/24`   
3. Use a `.tfvars` to pass the values from a file. (Recommended)   
   
   - `terraform.tfvars` - this is a file that contains the (keys)values for the variables. (If you don't pass a file name, it'll look for this file)   
   - Use the `-var-file` flag to pass the file name.   
     - `terraform apply -var-file terraform-dev.tfvars`   
 - `variables.tf` - is used to DEFINE variables NOT DECLARE inside the file whereas `.tfvars` is used to PASS variables. You can still declare a default value inside `variables.tf`   
 - Precedence → `.tfvars` → environment variables → `variables.tf`   
   
### Default values   
   
Default value will kick in if terraform cannot find the value in the `.tfvars` file or as a command line argument. A default value makes the variable optional.   
   
### Type constraints   
   
`type` specifies what value types the variable can accept.   
   
Using `list`:   
   
```json
variable "cidr_blocks" {
  description = "CIDR blocks list"
  type = list(string)
}

resource "aws_subnut" "dev-subnet-1" {
  vpc_id = aws_vpc.test_vpc.id
  cidr_block = var.cidr_blocks[1]
  availability_zone = "us-east-1a"
  tags: {
    Name: "subnet-1-dev"
  }
}
```
   
   
You can also use objects or lists of objects. You can also validate the type of the value for the objects as well.   
   
```json
// terraform-dev.tfvars

cidr_blocks = [
  {cidr_block = "10.0.10.0/16", name = "dev_vpc"},
  {cidr_block = "10.0.20.0/24, name = "dev_subnet"}
]
```
   
   
```json
variable "cidr_blocks" {
  description = "CIDR blocks list and Name tag"
  type = list(object({
    cidr_block: string
    name: string
  }))
}

resource "aws_vpc" "test_vpc" {
  cidr_block = var.cidr_blocks[0].cidr_block
  tags = {
    Name: var.cidr_blocks[0].name
  }
}
```
   
   
## Environment Variables   
   
Environment variables are defined by the providers for you to use.   
   
1. Use `export` to set the environment variable, it will be available only for the current shell session.   
   
   `export AWS_SECRET_ACCESS_KEY=<secret_access_key>`   
   `export AWS_ACCESS_KEY_ID=<access_key_id>`   
   
2. Set the environment variable in the `~/.aws/credentials` to be available globally, you may also use `aws configure` to set the credentials.   
   
### TF Environment Variable   
   
Define your own custom variables and use `.tf_var` to pass them to the Terraform configuration as global environment variables.   
   
   
- Define the variable - `export TF_VAR_my_custom_variable="my_custom_value"`   
- To use it, reference it without the `TF_VAR_` prefix.   
   
```json
variable "my_custom_variable" {}

resource "aws_subnut" "dev-subnet-1" {
  vpc_id = aws_vpc.test_vpc.id
  cidr_block = var.cidr_blocks[1]
  availability_zone = var.my_custom_variable
  tags: {
    Name: "subnet-1-dev"
  }
}
```
   
   
   
---   
   

   
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
   
   
   
---   
   
When you need to execute some sort of commands/shell scripts on the virtual servers that you have provisioned using Terraform. You can do so using `user_data` attribute but this method doesn't return any output. If anything goes wrong, you'd have to check directly from the machine by [ssh](../devlog/ssh.md)ing into it.   
   
But there's a better way of executing commands using Terraform on virtual servers using:   
   
## Provisioners   
   
Provisioners can be used to model specific actions on the local machine running the Terraform Core or on a remote machine to prepare servers or other infrastructure objects. But HashiCorp states in its documentation that they should be used as the last solution!   
   
### Null resource   
   
From the Terraform docs:   
   
The null provider is a rather-unusual provider that has constructs that intentionally do nothing. This may sound strange, and indeed these constructs do not need to be used in most cases, but they can be useful in various situations to help orchestrate tricky behavior or work around limitations.   
   
The documentation of each feature of this provider, accessible via the navigation, gives examples of situations where these constructs may prove useful.   
   
Usage of the null provider can make a Terraform configuration harder to understand. While it can be useful in certain cases, it should be applied with care and other solutions preferred when available.   
   
The Terraform `null_resourceis` commonly used to run scripts on a specified trigger.   
   
### Connection attribute   
   
It is a provisioner that allows us to connect to a server and execute commands on that server.   
   
`remote-exec` provisioners require connection credentials to function, even though `remote-exec` might be defined in a resource block that is a server, it doesn't connect to it unless explicity defined.   
   
### `remote-exec` provisioner   
   
This provisioner invokes a script on the newly created resource. it’s similar to connecting to the resource and running a bash or a command in the terminal.   
   
It can be used inside the Terraform resource object and in that case it will be invoked once the resource is created, or it can be used inside a null resource which is my prefered approche as it separates this non terraform behavior from the real terraform behavior.   
   
   
- Invokes script on a remote resource after it is created.   
   
   
- `inline` provisioner - list of commands   
- `script` provisioner - path to script   
- `file` provisioner - to copy files or directory from local to newly created resource   
  - If you want to copy the file to multiple machines you can have nested connection blocks inside the `file` provisioner.   
- `local-exec` - run commands locally NOT on the created resource.   
  - invokes a local executable after a resource is created.   
  - is invoked on the machine running TF, not on the resource!   
   
```terraform
resource "null_resource" "configure-vm" {

  connection {
      type = "ssh" # there are different types of connections
      user = var.username
      host = var.ip_address # you can also refer to self such as `self.public_ip`
      private_key = var.tls_private_key
    }

  ## Copy files to VM :
  provisioner "file" {
    source = "/Users/zakariaelbazi/Documents/GitHub/zackk8s/kubernetes" #TODO move to variables.
    destination = "/home/${var.username}"
  }

  ## install & start minikube
  provisioner "remote-exec" {
    inline = [
      "sudo chmod +x /home/${var.username}/kubernetes/install_minikube.sh",
      "sh /home/${var.username}/kubernetes/install_minikube.sh",
      "./minikube start --driver=docker"
    ]
  }
}
```
   
   
> Note that you can not pass any arguments to the script or command, so the best way is to use file provisioner to copy the files to the resources and then invoke them with the remote-exec provisioner like I did above for my script that installs minikube on the azure-vm.   
   
> An other thing to pay attention to is that by default, provisioners that fail will also cause the Terraform apply to fail. To avoid that, the on_failure can be used.   
   
```terraform
resource "null_resource" "configure-vm" {
    .........
    ..........

  provisioner "remote-exec" {
    inline = [
      "sudo chmod +x /home/${var.username}/kubernetes/install_minikube.sh",
      "sh /home/${var.username}/kubernetes/install_minikube.sh",
      "./minikube start --driver=docker"
    ]
    # you can also use script instead of inline, the script should already exist on the server!
    # you'll use the file provisioner to copy the script to the machine first.
    on_failure = continue #or fail

  }
}
```
   
   
In this example, I am using inline; which is a series of command, the `on_failure` will apply only to the final command in the list !   
   
### `local-exec` provisioner   
   
Technically, this one is very similar to the one before in terms of behavior or use but it works in the local machine ruining Terraform. It invokes a script or a command on local once the resource it’s declared in is created.   
   
It’s the only provisioner that doesn’t need any [ssh](../devlog/ssh.md) or [winrm](../devlog/winrm.md) connection details as it runs locally.   
   
### Disclaimer for Provisioners   
   
HashiCorp states in its documentation that they should be used as the last solution! and even Nana doesn't recommend using it. But there might be some use cases for them.   
   
Use `user_data` when you can.   
   
**Provisioners breaks idempotency.** Terraform doesn't understand the current state or the future state because it has no idea what you're executing. Breaks current state-desired state comparison.   
   
### Best practices when using Provisioners   
   
   
- When you want to execute commands remote/configure a server, use a configuration management tool instead.   
  - Once server is provisioned, hand over the rest to the config management tool with some init data.   
- An alternative to `local-exec` is `local` provider.   
  - Provider is able compare states, the declarative model is kinda maintained this way.   
- Execute scripts separate from Terraform, maybe from from CI/CD Pipeline tool such [Jenkins](../devlog/jenkins.md).   
   
### Provisioner Failure   
   
   
- Terraform will mark or taint the resource when a provisioner fails.   
   
   
---   
   
## Modules   
   
Not using modules in our `.tf` files will result in complex configurations with huge file sizes and no overview. We don't want our terraform files to be monolithic, we want them to be modular for better organization.   
   
We should encapsulate them into distinct logical components(resources) for better reusability.   
   
A high level example of a module could be a module that contains all the things(**group of resources**) you need for spinning up an a web server, which can be reused in your other modules and vice versa which helps with keeping your code [DRY](../devlog/DRY.md). This module can also be parameterized using variables and make it output values such as exposing created resources or specific attributes. **A module as function definition. Input variables like function arguments and output variables like function return values.**   
   
We can create our own modules but for the most common use cases, Terraform and other organizations, individuals have already created some modules for us to use.   
   
   
- [Browse Modules | Terraform Registry](https://registry.terraform.io/browse/modules)   
   

   
It is a common practice to have different files for variables, outputs, providers respectively.   
   
Theres no such thing as imports in Terraform to be made in `main.tf` file. Terraform automatically takes care of the importing. The file names are named as they're because of convention, you can name them whatever you want.   
   
**Creating modules is basically grouping multiple resources into one logical unit to make them reuseable.**   
   
## Structure   
   
When creating a module it should group a couple of resources together, creating a module for one or two resources doesn't really make much sense.   
   
   
- The root module will have `main.tf`.   
- `/modules` - is where all the child modules belong.   
- A "child module" is a a module that is called by another configuration.   
   
## Create a Module   
   
   
- Create a folder named "modules".   
- Create subfolders under "modules" such as "webserver", "subnet".   
  - These subfolders will have their own `main.tf`, `variables.tf` and `outputs.tf`.   
   
## Use a Module   
   
   
- To reference a module in another module or in the main `main.tf` is using `module` keyword.   
- define all the variables that you're going to use in the modules; first inside `variables.tf` and set the values using `terraform.tfvars`, and reference them as attribute names for the module from `terraform.tfvars`. The variable in the module can be hardcoded or it can be referenced from `.tfvars` or it can be referenced from a resource object.   
   
```terraform
module "myapp-subnet"{
  source = "./modules/subnet" # relative-path-to-module
  avail_zone = var.avail_zone
  vpc_id = aws_vpc.myapp-vpc.id
  default_route_table_id = aws_vpc.myapp-vpc.default_route_table_id
}
```
   
   
## Module Output   
   
When you're trying to reference a resource name for a value that isn't part of the module you're working in, the child module resource can only be access from module definition.   
   
To access the resource of a child module, you need to expose/export resource attributes to parent module. You can do this using `outputs.tf`   
   
```terraform
output "subnet" {
  value = aws_subnet.myapp-subnet-1 # will output the whole subnet object
}
```
   
   
This "subnet" object can now be referenced in any other resource in a parent module.   
   
```terraform
# parent main.tf

resource "aws_instance" "myapp-server" {
  ...
  ...
  subnet_id = module.myapp-subnet.subnet.id # subnet = outputted object
}
```
   
   
**To apply configuration** you need to run `terraform init` whenever a module has been changed or added before you run `terraform plan` & `terraform apply`.   
   
   
- Example module can be found at [feature/modules · zubayrrr · GitLab](https://gitlab.com/zubayrrr/terraform-learn/-/tree/feature/modules)
   
   
## Errors   
   
When an error occurs a `crash.log` file is created in the root directory of your Terraform config.   
It will have all the logs of failures of `terraform apply`.   
   
## Remote State   
   
State can be created in multiple places, like state for different team members working on something or in a CI/CD pipeline.   
   
The problem is that every user/CI server must make sure they've the latest state data before running Terraform.   
   
So how do you sync/share Terraform state between different teams/env.   
   
Enter **Remote State**   
   
   
- TF writes the data to this remote data store.   
- Different remote storage options available.   
   
It also helps with:   
   
   
- data backup   
- can be shared   
- keeps sensitive data off disk   
   
**Configure remote state**   
   
In `main.tf`'s `terraform{}` block we can define metadata.   
   
Example using [aws.s3](../devlog/aws.S3.md)   
   
```tf
terraform{
  required_version = ">=0.12"
  backend "s3"{
    bucket = "myapp-bucket"
    key = "myapp/state.tfstate"
    region = "eu-west-3"
  }
}
```
   
   
Create an S3 bucket in your AWS account. Make sure to block public access.   
   
## Labs   
   
   
- [terraform.Automate Provisioning EC2](../devlog/terraform.Automate%20Provisioning%20EC2.md)   
- [terraform.Automate Provisioning EKS cluster](../devlog/terraform.Automate%20Provisioning%20EKS%20cluster.md)   
- [terraform.ci∕cd with Terraform](../devlog/terraform.ci%E2%88%95cd%20with%20Terraform.md)   
   
## Resources   
   
   
- [What is terraform provisioner? | Jhooq](https://jhooq.com/terraform-provisioner/)   
- [All you need to know about Terraform provisioners and why you should avoid them. | AWS Tip](https://awstip.com/all-you-need-to-know-about-terraform-provisioners-and-why-you-should-avoid-them-22b5ef8d2db2)   
- [Terraform Tutorial: Drift Detection Strategies](https://www.trendmicro.com/ru_ru/devops/22/c/terraform-tutorial-drift-detection-strategies.html)   
   
## Misc   
   
   
- `versions.tf` - you can provide the version of your provider(AWS, GCP etc or Custom providers)   
- `random_string` (Resource) - The resource `random_string` generates a random permutation of alphanumeric characters and optionally special characters.   
- `locals` - `common_tags`, `default_tags`   
- merge function