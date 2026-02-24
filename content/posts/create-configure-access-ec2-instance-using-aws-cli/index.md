---
id: "PQB5EY7fT5ShQEcjBNaDCQ"
status: "published"
createdAt: "2024-08-13T13:13:46+01:00"
firstPublishedAt: "2024-08-13T13:50:14+01:00"
publishedAt: "2024-08-22T16:11:32+01:00"
updatedAt: "2024-08-22T16:11:19+01:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/growtika-tkag3wignsw-unsplash.jpg"
date: "2024-08-13"
excerpt: "How to edit, create and configure an EC2 instance in AWS."
slug: "create-configure-access-ec2-instance-using-aws-cli"
title: "Create, configure & access EC2 instance using AWS CLI"
---

# Create, configure & access EC2 instance using AWS CLI

## Introduction 

In this post I gonna explain you the steps to work with an EC2 instance in AWS. EC2 is a virtual machine in the cloud. you have more information here [https://aws.amazon.com/de/ec2/](https://aws.amazon.com/de/ec2/)

Besides the fact that it is a virtual machine in AWS Cloud and that we will use AWS Cli to interact with it, there is few differences from setting up a virtual machine in other environments \(on premise, locally etc..\)

As said above, we will use AWS Cli for interact with our EC2 instance in AWS. AWS Cli is a Command line tool that allows to do anything with AWS. All what we will do could be also done with the AWS UI \(web appliction in aws.mazon.es\) but I prefer to work with the command line as I can document and store the commands and steps required. 

For installing and configuring the tool pleas refer [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/). You will need to download it, login in as an user with permit to execute all the commands needed for creating / managing / configuring an EC2 instance. I will not go in the details of doing it, so maybe you need to google a bit first to configure properly your AWS Cli. Sorry about it. 

## Creating an EC2 Instance

The command to create an EC2 instance using AWS CLI is the following

```bash
aws ec2 run-instances \
    --image-id <image_id> \
    --count 1 \
    --instance-type <instance_type> \
    --key-name ec2-key-pair \
    --security-group-ids <security_group_id> \
    --subnet-id <subnet_id> \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=MyUbuntu24Server}]'
```

Let's go step by step for this command: 

`aws ec2 run-instances` 

it is the command itself to instruct AWS to create an EC2 instance

`--image-id`

When you create a new virtual machine, you need to define an image where this virtual machine will be created from. For example in my case my virtual machine will be baed in a linux Ubuntu 22.4 OS 

AWS provides a lot of images to choose from. Just check the catalog \(for your current Region!\)  `https://eu-west-3.console.aws.amazon.com/ec2/home?region=eu-west-3\#AMICatalog:`

The linux Ubuntu 22.4 OS has this id: `ami-09d83d8d719da9808`

`--count 1`  

we are here just indicating we want to create 1 new virtual machine. 

`--instance-type`

Virtual machine can have different setup in regards memory, hard disk and so on. in my case I want a `t3.small` 

`--key-name` this is related to the SSH key you need to provide to connect to your virtual machine by SSH in a later stage 

> Connecting to the EC2 using this method it is not the same as connecting to the virtual machine as root user. This is higher level connection provided by AWS itself.
>
>

```bash
# Create the key
aws ec2 create-key-pair --key-name ec2-key-pair --query 'KeyMaterial' --output text > ec2-key-pair.pem
# move it to your .aws directory (it was created when setting up the AWS Cli)
mkdir -p ~/.aws/keys
mv ec2-key-pair.pem ~/.aws/keys/
```

`--security-group-ids`

This is a layer of security on top EC2. Any VM needs a security group to be related to. In the security group you can define things like opened / closed ports and so on. 

> It is like a AWS Fire wall level.
>
>

Use this query to get your available security groups ids, just get one.  

```bash
aws ec2 describe-security-groups --query "SecurityGroups[*].[GroupId,GroupName]"`
```

`--subnet-id` 

A subnet is basically the data center hosting your Virtual Machine. As for security group, run the following command and get the ids id of the subnet you want to attach your VM to.

```bash
aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-0fc610e648a8bcb9f"
```

Once you have all in place we can fill the holes to get the final command to be run:

```bash
aws ec2 run-instances \
    --image-id ami-09d83d8d1234556 \
    --count 1 \
    --instance-type t3.small \
    --key-name ec2-key-pair \
    --security-group-ids sg-075feffa6123456 \
    --subnet-id subnet-041c6e8d1234566 \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=MyUbuntu24Server}]'
```

Instance created!! \(you should have an id as response back\)

Check the instance by running:

```bash
# Get all your EC2 instances
aws ec2 describe-instances

# Details of the instance by id
aws ec2 describe-instances --instance-ids i-078efac1231345
```

## Configure Access to EC2 Instance

Now we have the instance created and we can connect using our AWS key, later on we will configure users and try to connect through the browser but for it first of all you need to do two things:

### Configure a public IP address

```bash
aws ec2 associate-address --instance-id <instance_id> --allocation-id <allocation_id>`
```

where `instance\_id` is the id of the instance you created and `allocation id` can be found running this command: 

```bash
ws ec2 allocate-address --domain vpc 
```

- Open ports in the Security Group \(22 for SSH and 80 for HTTP\)

```bash
# allow access through port 22
## get the public IP if your laptop
MY_IP=$(curl -s ifconfig.me)
aws ec2 authorize-security-group-ingress --group-id sg-123123123
--protocol tcp --port 22 --cidr $MY_IP/32

# Allow access prt 6443 (for K8S in case you need it)
aws ec2 authorize-security-group-ingress --group-id sg-123123123 --protocol tcp --port 6443 --cidr 0.0.0.0/0 

# and allow access through port 80
aws ec2 authorize-security-group-ingress --group-id sg-123123123 --protocol tcp --port 80 --cidr 0.0.0.0/0
```

> As you have most probably a public dynamic IP is possible that you need to update this rule from time to time...
>
>

## Configure EC2 Instance

Once you have the instance in place and access properly configured, configuring a EC2 does not differ to configure any public virtual machine.

You need: 

- Update Packages \(with apt-get if it is a Ubuntu instance\)
- Set up nd configure a Firewall
- Create a configure SSH Users to connect / Disable Root Login
- \(Optional\) Add monitoring and and security tools 

These are a bunch of commands to be run directly in the server. For documentation I gonna leave them here but I will not go in detail in each of them.



```bash
# update system
sudo apt update sudo apt upgrade -y

# setup and configure firewall
sudo apt install ufw -y 
sudo ufw default deny incoming 
sudo ufw default allow outgoing 
sudo ufw allow ssh 
sudo ufw allow http 
sudo ufw enable sudo ufw allow 6443/tcp # for K8S
sudo ufw enable

# new ssh user and disable root
sudo adduser vicens 
sudo usermod -aG 
sudo vicens
sudo nano /etc/ssh/sshd_config # in the file set `PermitRootLogin no`
sudo systemctl restart ssh # restart SSH

## in your local machine create SSH key to connect to the server 
ssh-keygen -t rsa -b 4096 -C "my_email@emil.com"
cat ~/.ssh/id_rsa.pub # copy key to clipboard

# in the VM
sudo su - vicens 
mkdir -p ~/.ssh 
chmod 700 ~/.ssh
nano ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
sudo systemctl restart ssh # restart ssh

# After doing it you should be able to connect to the VM from your local machine
ssh -i ~/.ssh/id_rsa vicens@ec1234-22-23.eu-west-3.compute.amazonaws.com

# Add fail2ban
```shell
sudo apt install fail2ban -y 
sudo systemctl start fail2ban 
sudo systemctl enable fail2ban

# automatic updates
sudo apt install unattended-upgrades -y 
sudo dpkg-reconfigure --priority=low unattended-upgrades

# Monitoring tools
sudo apt install logwatch htop -y 
sudo logwatch --output mail --mailto datracka@gmail.com --detail high

# for fun just add an apache
sudo apt install apache2 -y 
sudo nano /etc/apache2/apache2.conf 
# (Remove Options -Indexes) in <Directory /var/www/>. To avoid list the files in the server

sudo nano /etc/apache2/conf-available/security.conf 
# (Set ServerTokens Prod and ServerSignature Off) 

sudo apt install libapache2-mod-security2 -y 
sudo a2enmod security2 
sudo systemctl restart apache2
```

## Summary

If you have reach this point you should have a ready virtual machine running using Ubuntu 22.4 in AWS Cloud EC2 Instance and you could connect either using your AWS level SSH key or the user you created in the instance itself. 

```bash
ssh -i ~/.ssh/id_rsa vicens@ec2-15-2123123232.eu-west-3.compute.amazonaws.com
```

Remember that the instance name `ec2-15-2123123232.eu-west-3.compute.amazonaws.com` can be found using the `describe instance` commands from above..

I hope it was helpful to you!
