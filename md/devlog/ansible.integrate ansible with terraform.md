---
created: 1661337943858
desc: ''
id: 3b3s4928t5qon4eonq82svo
title: Integrate Ansible with Terraform
updated: 1661688034084
---
   
**Integrate Ansible Playbook Execution in [Terraform](../devlog/terraform.md)**   
   
What we've seen thus far:   
   
   
- Provisioning of an instance using Terraform.   
- Configuration of EC2 instance using Ansible.   
   
It isn't completely automated as there are still manual steps involved:   
   
   
- We get the IP address manually from TF output.   
- Update the hosts file manually.   
- Execute Ansible command.   
   
Let's automate everything from instantiating EC2 server, handing it over to Ansible for configuring the server with one just command i.e `terraform apply`.   
   
Let's write the "handover to Ansible" code inside Terraform.   
   
   
- [View the finished Terraform code on Gitlab](https://gitlab.com/zubayrrr/terraform-learn/-/tree/feature/ansible)   
- [View the finished Ansible code on GitLab](https://gitlab.com/zubayrrr/ansible-learn/-/blob/master/deploy-docker-new-user.yaml)   
   
**`local-exec` and `null_resource` in Terraform**   
   
```t

/*
provisioner "local-exec" {
    working_dir = "../ansible"
    command = "ansible-playbook --inventory ${self.public_ip}, --private-key ${var.ssh_key_private} --user ec2-user deploy-docker-new-user.yaml"
  }
}
/*


resource "null_resource" "configure_server" {
  triggers = {
    trigger = aws_instance.myapp-server.public_ip
  }

  provisioner "local-exec" {
    working_dir = "../ansible"
    command = "ansible-playbook --inventory ${aws_instance.myapp-server.public_ip}, --private-key ${var.ssh_key_private} --user ec2-user deploy-docker-new-user.yaml"
  }
}
```
   
   
**Ensure EC2 has successfully initialized**   
   
```yaml
---
- name: Wait for ssh connection
  hosts: all
  gather_facts: False
  tasks:
    - name: Ensure ssh port open
      ansible.builtin.wait_for:
        port: 22
        delay: 10
        timeout: 100
        search_regex: OpenSSH
        host: "{{ (ansible_ssh_host|default(ansible_host))|default(inventory_hostname) }}"
      vars:
        ansible_connection: local
        ansible_python_interpreter: /usr/bin/python
```
