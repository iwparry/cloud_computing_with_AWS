# AWS Services/Products
AWS offers its users a wide range of products including compute, storage, database and more.

This markdown provides some overview of some of the many cloud products on offer to AWS users.

## IAM  - Identity and Access Management
IAM is an example of a Global service in AWS (available in all AWS regions). IAM allows you to specify who or what can access services and resources in AWS and centrally manage permissions that control which AWS resources users can access.
## EC2 - Elastic Compute Cloud
One of the most popular services AWS has to offer. Amazon EC2 is a web service that provides resizable computing capacity that you use to build and host your software systems. Some of its features include virtual computing environments (instances), preconfigured templates for your instances (AMIs) and more.

## EBS Volume - Elastic Block Store
An EBS Volume is a network drive that we can attach to our running EC2 Instances, allowing them to persist data, even beyond termination. These are bound to specific availability zones, i.e. we cannot attach an EBS Volume in eu-west-1a to an instance in eu-west-1b.

## AMI - Amazon Machine Image
AMI is a customisation of an EC2 instance. We can launch EC2 instances from either a public AMI (provided by AWS) or we create and maintain our own AMIs containing our own software, configuration, operating system etc. There is also the option to launch an EC2 instance from an AWS Marketplace AMI, which is an AMI that has been made by someone else.

## EC2 Image Builder
Is a service used to automate the creation of VMs or container images. This allows us to automate the creation, maintenance, validation and testing of EC2 AMIs.

## EFS - Elastic File System
Is a managed network file system that can be mounted on hundreds of instances. These work with Linux EC2 instances in mulitple availability zones. Everything on the EFS drive is shared by everything mounted to it making it a shared file system, unlike EBS. There is a class of storage in EFS which is EFS Infrequent Access, which is cost-optimised for files that are not accessed every day, in this class EFS will automatically move your files to EFS-IA based on when they were last accessed.

## Amazon FSx
This is a fully managed service which is a network file system, offerings of this service include FSx for Windows File Server which provides fully managed Microsoft Windows file servers, backed by a fully native Windows file system.

## Elastic Load Balancing (ELB)
Load balancers are servers that direct traffic to multiple servers (EC2 Instances) downstream. This allows traffic to be spread across multiple downstream instances, and is done so in a way that not one single instance is overwhelmed. There are several types of load balancers in AWS being Application, Network and Gateway.

Key characteristics of each load balancer type:

Application Load Balancer
- HTTP/HTTPS/gRPC protocols (layer 7)
- HTTP Routing features
- Static DNS (URL)

Network Load Balancer
- TCP/UDP protocols (layer 4)
- High Performance
- Static IP through Elastic IP

Gateway Load Balancer
- GENEVE protocol on IP Packets (layer 3)
- Route Traffic to Firewalls that you manage on EC2 Instances
- Intrusion detection

## Auto Scaling Groups (ASG)
Allows us to scale out/in automatically based on load to ensure that our websites and application are able to match demand at any given time.