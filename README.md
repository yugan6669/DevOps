# DevOps    =  Dev  +  Ops   =   Development + Operations
 
This project is implemented to touch and feel the DevOps Pipeline


# Phase 0: launch ec2 instance and named as "Sandbox"

Step 1: Launch EC2 instance from the AWS Console and logging into EC2 instance and clone the deployer git repo

$sudo yum install git -y

$sudo git clone https://github.com/krishnamaram2/deployer.git

Step 2: Install all the necessary packages  

$python ./deployer/src/sandbox/sandbox.py

Step 3: Configuring AWS CLI

$python ./deployer/src/aws/aws-config.py


# Phase 1: Build custom AMI using "Packer"

$python ./deployer/src/packer/packer.py


# Phase 2: Build infrastructure using "Terraform"

$python ./deployer/src/terraform/terraform.py


# Phase 3: Run the Playbooks using Ansible 

$python ./deployer/src/ansible/ansible-playbooks.py
