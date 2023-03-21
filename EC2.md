# EC2 - Elastic Compute Cloud
In AWS EC2 allows users to create virtual servers

## Creating an EC2 Instance
An EC2 Instance is a virtual machine that we can create in the cloud, the setup of an EC2 instance covers several components

### AMI (OS)
A preconfigured template for your instances, known as _Amazon Machine Images_, that package your server requirements (including the operating system and additional software). Amazon provides several of these already but we can create our own AMIs based off of instances we have configured.

### Instance Types
Standard `t2.micro`

### Setting Security Groups
A Security Group is a firewall that we attach to an EC2 instance, this controls the traffic heading in and out of our instance.

Note with security groups, if connecting to an instance fails due to a timeout, this implies a security group issue.

### Classic Ports to know
- 22 = SSH (Secure Shell) - log into a Linux instance
- 21 = FTP (File Transfer Protocol) - upload files into a file share
- 22 = SFTP (Secure File Transfer Protocol) -  upload files using SSH
- 80 = HTTP - access unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP (Remote Desktop Protocol) - log into a Windows instance

### User Data
This feature allows us to bootstrap our instance, meaning that we provide a script to be executed inside our instance when its launched for the first time (Note to start the script off with `#!/bin/bash`)

### EC2 Instance Role
This allows us to link an EC2 instance to an IAM role, allowing us to interact with the AWS console via `awscli` (provided that the role has the permissions to do so).