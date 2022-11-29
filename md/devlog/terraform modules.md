---
created: 1660823604600
desc: ''
id: h61xyexpa9vbpku7et1x6k8
title: Terraform Modules
updated: 1660991090783
---
   
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