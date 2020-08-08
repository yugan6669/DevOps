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



# Phase 1: Build custom AMI using "Packer"

Step 1: Configuring AWS CLI

$aws configure

Step 2:clone the git repo

$git clone https://github.com/krishnamaram2/deployer.git

Step 3: execute command 

$python ./deployer/src/packer/packer.py



# Phase 2: Build infrastructure using "Terraform"


step 0: create the below objects in AWS

create s3 bucket

create file under above s3 bucket

create DynamoDB table

step 1: clone repo

$git clone https://github.com/krishnamaram2/Infrastructure_Manager.git


Step 2: move to directory

cd Infrastructure_Manager/src



Step 3: enter access key and secret key in the below files 

$vi backend.tf

terraform{

backend "s3"{

access_key = ""

secret_key = ""

region = "us-east-1"

bucket = "<<mybucket>>"

key = "<<myfile>>"

dynamodb_table = "<<mytable>>"

}

}


$vi config.json

{

"myregion" : "us-east-1",

"myaccesskey" : "",

"mysecretkey" : "",

"myamiid" : ""

}


Step 4:

$terraform init .

$terraform validate -var-file=config.json .

$terraform apply -var-file=config.json .


# DevStack

this project is implemented to touch and feel CICD pipeline

# Phase 3: Installing and configure using "Ansible"


Step 0: add public keys


step 1: clone repo

$git clone https://github.com/krishnamaram2/Configuration_Manager.git

Step 2:

$cd Configuration_Manager/src/plays

$ansible-playbook -i hosts devstack.yml




# OpsStack

This project implemented to touch and feel 3-tier Distributed/Containerized  webapp communication flow 


# Phase 3: Installing and configure using "Ansible"


Step 0: add public keys


step 1: clone repo

$git clone https://github.com/krishnamaram2/Configuration_Manager.git

Step 2:

$cd Configuration_Manager/src/plays

$ansible-playbook -i hosts opsstack.yml



