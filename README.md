# Project-Ansible-Jan-12
The aim of this project is to deploy install apache, update patches and copy html files  to targets servers using Ansible.

Description
Terraform was used to build AWS resources ( ansible master and ansible hosts)

Requirements
AWS Cli and have a IAM profile configured
Terraform
Ansible 
SSH Access to the target servers (2 hosts)

Once the infrastructures are built, we need to obtain the Private-IP addresses of the target servers
using the following commands:

webserver1=$(terraform output -raw webserver-private-ip)
webserver2=$(terraform output -raw webserver-private-ip1)

Login into the Ansible-master to generate new key-pairs

sudo ssh-keygen -t rsa -b 2048 -f ~/.ssh/ <public key name>

#Copy the public key into the target servers as new user ansadmin
sudo ssh-copy-id -i ~/.ssh/ansible_key.pub ansadmin@$webserver1
sudo ssh-copy-id -i  ~/.ssh/ansible_key.pub ansadmin@$webserver2

#Copy the target servers into the ansible inventory file
$webserver1 > inventory
$webserver2 >> inventory 

Usage:
run the command ansible-playbook -i < inventory> <playbook_name>.yml 
