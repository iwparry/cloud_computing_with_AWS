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

## Elastic Block Store (EBS) Volume
These volumes are network drives (i.e. not physical) that we can attach to our running EC2 Instances, allowing them to persist data, even beyond termination. We can think of these as USB Sticks for our intsances. These will be created with our instances but we can create them ourselves and attach them to our instances. We can attach multiple volumes to our instances. Note that volumes are bound by availability zones, thus we cannot attach to instances outside an EBS Volume's AZ. 

We can view and manage our volumes by clicking on "Volumes" in the "Elastic Block Store" dropdown on the left-hand side of the AWS console

## Amazon Machine Image (AMI)
When we create an instance we need to select an AMI, these can be provided to us by AWS in the form of Public AMIs, but we do have the option in AWS to create our own AMIs that will contain our desired OS, software, configurations etc. We can think of this as creating a template based on a customised EC2 instance. 

## Scalability
Scalability refers to the ability to adapt based on demand. There are two types of scalability.
### Vertical Scalability
This means increasing the size of the instance, i.e. scale up or down, e.g. if our application is running on t2.micro we can vertically scale that application meaning that the instance the application runs on increases to t2.large. Note with vertical scalability there is a limit on how much we can vertically scale, which is the hardware limit.
### Horizontal Scalability
This means increasing the number of instances running for our application, i.e. scale in and out. This is very common for modern applications as many of these are developed with horizontal scalability in mind. It is possible to achieve this in AWS via Auto Scaling Groups and Load Balancers.

## High Availability
High availability in AWS means running your application in at least 2 AZs, this is a measure to counter data centre loss (such as via natural disasters).

## Elasticity
This means once a system is scalable there will be some auto-scaling so that the system can scale based on the load so that it is able to match demand.

## Application Load Balancer (ALB)
We can create a load balancer to direct the traffic among our targeted EC2 instances. This also supports health checks of our EC2 instances.

## Auto Scaling Group (ASG)
The goal of an ASG is to:
- Scale out (add EC2 instances) to match an increased load
- Scale in (remove EC2 instances) to match a decreased load
- Ensure we have a minumum and a maximum number of machines running
- Automatically register or deregister instances to a load balancer
- Replaces unhealthy instances

ASG and load balancers go hand in hand!