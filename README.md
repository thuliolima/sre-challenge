# sre-challenge


1 - To do this challenge it is necessary to meet the requirements below:

    1.1 - Get a valid AWS account => aws.amazon.com.br

    1.2 - After having the valid account, it is necessary to create a user with permissions to create and access the EC2 services and create a .pem 
    type key to access the ec2 instances, and for that it is necessary to follow the document below:

        1.2.1 - https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/id_users_create.html#id_users_create_console
        1.2.2 - https://docs.aws.amazon.com/ground-station/latest/ug/create-ec2-ssh-key-pair.html

2 - Install ansible: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

3 - Perform terraform installation: https://learn.hashicorp.com/tutorials/terraform/install-cli


4 - Enter the terraform folder and perform the following settings:
    
    4.1 - Open the variables.tf file and change the line below:

            variable "key_name" {
                description = " SSH key connect to ec2 instance"
                default = "name-key"
            }

    4.2 - Open the main.tf file and change the lines below:

            provider "aws" {
                region = var.aws_region
                access_key = "XXXXXXXXXXXXXXXXXXXXX"
                secret_key = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
            }

5 - After the steps above, we will perform the necessary commands to provision the infrastructure with terraform:

    terraform init
    terform plan
    terraform

    Note: the commands above are responsible for the following processes: configuring the AWS provider, reading the ec2 machine provisioning file and
    application of infrastructure provisioning on AWS.

6 - After step 5, let's go some configurations for ansible connections to the provisioned ec2.

    6.1 - Open the ansible folder and edit the hosts file.

        6.1.1 - Add ec2's public ip

        6.1.2 - Add the path of the .pem key that was created according to step 1.1.2.2.

           [sre_challenge:vars]
            ansible_ssh_private_key_file=/path/key.pem
            ansible_user=ubuntu
           [sre_challenge]
            #public IP
            x.x.x.x

7 - After the above just run the command "ansible-playbook -i ./hosts docker_playbook.yml -v"

8 - The end of the installations, just access the application through the public ip of ec2.