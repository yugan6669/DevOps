# DevOps    =  Dev  +  Ops   =   Development + Operations
 
This project is implemented to touch and feel the DevOps Pipeline


# Pre-Requisites

# Phase 0: launch ec2 instance to build Infra and named as "Sandbox"

Step 1: Launch EC2 instance from the AWS Console

Step 2: Logging into EC2 instance and clone the git repo

$sudo yum install git -y

$git clone https://github.com/krishnamaram2/deployer.git

Step 3:
$python ./deployer/src/sandbox/sandbox.py

Step 1: Configuring AWS CLI

$$python ./deployer/src/aws/aws-config.py


# Phase 1: Build custom AMI using "Packer"

$python ./deployer/src/packer/packer.py


# Phase 2: Build infrastructure using "Terraform"

$python ./deployer/src/terraform/terraform.py



# OpsStack

This project implemented to touch and feel 3-tier Distributed/Containerized  webapp communication flow 


# Phase 3: Installing and configure using "Ansible"


Step 0: add public keys

 #!/bin/bash
 
 ssh-keygen -q -t rsa -N '' -f /home/centos/.ssh/id_rsa <<<y 2>&1 >/dev/null

 cat /home/centos/.ssh/id_rsa.pub >> /home/centos/.ssh/authorized_keys

 ssh -o StrictHostKeyChecking=no centos@localhost


step 1: clone repo

$git clone https://github.com/krishnamaram2/Configuration_Manager.git

Step 2:

$cd Configuration_Manager/src/plays

$ansible-playbook -i hosts opsstack.yml

$ansible-playbook -i hosts devstack.yml

$ansible-playbook -i hosts webapp.yml





