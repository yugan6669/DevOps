# DevOps    = Development + OPerations
 




# devstack
This project implemented to touch and feel CICD Pipeline 

# Phase 0: lauch ec2 instance and named as "Sandbox"

step 0: login to sandbox instance

step 1: repo file

$vi ansible.repo

[Ansible]

name = ansible

baseurl = https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/

enabled = 1

gpgcheck = 0

step 2: install packages

$vi setup.sh

yum update -y && yum upgrade -y

yum install git -y && yum install wget -y && yum install unzip -y && yum install curl -y && yum install epel-release -y

wget https://releases.hashicorp.com/packer/1.5.5/packer_1.5.5_linux_amd64.zip && unzip packer_1.5.5_linux_amd64.zip && mv packer /bin/ && rm -rf ./packer*

wget https://releases.hashicorp.com/terraform/0.12.24/terraform_0.12.24_linux_amd64.zip && unzip terraform_0.12.24_linux_amd64.zip && mv terraform /bin/ && rm -rf ./terraform* 

sudo cp ./ansible.repo /etc/yum.repos.d/

yum install ansible -y

step 3: run script

$sudo sh setup.sh 

# Phase 1: Build custome AMI image using "Packer"

step 1: clone repo

$git clone https://github.com/krishnamaram2/Image_Builder.git

step 2: enter src directory

$cd Image_Builder/src

step 3: enter access key and secret key

$vi variables.json

{

"aws_access_key": "",

"aws_secret_key": "",

"region": "us-east-1"

}

Step 4: validate syntax

$packer validate -var-file=variables.json builders.json

Step 5: Build custome AMI

$packer build -var-file=variables.json builders.json


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



# Phase 3: Installing and configure using "Ansible"


Step 0: add public keys


step 1: clone repo

$git clone https://github.com/krishnamaram2/Configuration_Manager.git

Step 2:

$cd Configuration_Manager/src/plays

$ansible-playbook -i hosts devstack.yml







# opsstack
This project implemented to touch and feel 3-tier Distributed/Containerized  webapp communication flow 

# Phase 0: lauch ec2 instance and named as "Sandbox"

step 0: login to sandbox instance

step 1: repo file

$vi ansible.repo

[Ansible]

name = ansible

baseurl = https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/

enabled = 1

gpgcheck = 0

step 2: install packages

$vi setup.sh

yum update -y && yum upgrade -y

yum install git -y && yum install wget -y && yum install unzip -y && yum install curl -y && yum install epel-release -y

wget https://releases.hashicorp.com/packer/1.5.5/packer_1.5.5_linux_amd64.zip && unzip packer_1.5.5_linux_amd64.zip && mv packer /bin/ && rm -rf ./packer*

wget https://releases.hashicorp.com/terraform/0.12.24/terraform_0.12.24_linux_amd64.zip && unzip terraform_0.12.24_linux_amd64.zip && mv terraform /bin/ && rm -rf ./terraform* 

sudo cp ./ansible.repo /etc/yum.repos.d/

yum install ansible -y

step 3: run script

$sudo sh setup.sh 

# Phase 1: Build custome AMI image using "Packer"

step 1: clone repo

$git clone https://github.com/krishnamaram2/Image_Builder.git

step 2: enter src directory

$cd Image_Builder/src

step 3: enter access key and secret key

$vi variables.json

{

"aws_access_key": "",

"aws_secret_key": "",

"region": "us-east-1"

}

Step 4: validate syntax

$packer validate -var-file=variables.json builders.json

Step 5: Build custome AMI

$packer build -var-file=variables.json builders.json


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



# Phase 3: Installing and configure using "Ansible"


Step 0: add public keys


step 1: clone repo

$git clone https://github.com/krishnamaram2/Configuration_Manager.git

Step 2:

$cd Configuration_Manager/src/plays

$ansible-playbook -i hosts opsstack.yml



