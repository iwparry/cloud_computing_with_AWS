# AWS Services/Products
AWS offers its users a wide range of products including compute, storage, database and more.

This markdown provides some overview of some of the many cloud products on offer to AWS users.

## IAM  - Identity and Access Management
IAM is an example of a Global service in AWS (available in all AWS regions). IAM allows you to specify who or what can access services and resources in AWS and centrally manage permissions that control which AWS resources users can access.
# EC2 - Elastic Compute Cloud
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

# Amazon Simple Storage Service (S3)
Advertised as "infinitely scaling" storage, Amazon S3 is an object storage service that offers scalability, data availability, security, and performance. Industries can use Amazon S3 to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, and more.

### Durability
This concept represents how many times an object is going to be lost by Amazon S3. S3 has incredibly high durability, it is said on average that if you store 10 million objects with Amazon S3, you can expect to lose a single object once every 10 thousand years.

### Availability
This measures how readily available a service is, this actually varies depending on what S3 storage class is used e.g. S3 Standard has 99.99% availability over a given year vs S3 One Zone-IA that has 99.5% availability over the same time period.

## AWS Snow Family
AWS Snow Family os a collection of physical devices that help migrate large amounts of data into and out of the cloud without depending on networks. This helps you apply the wide variety of AWS services for analytics, file systems, and archives to your data.

We have 3 types of device that make up the Snow Family being the AWS Snowcone, Snowball, Snowmobile.

### Data Migration
Transferring data via a network can take a lot of time and include challenges such as limited connectivity, bandwith, high network cost, shared bandwith etc. Amazon gives us a way around this by sending us physical devices where we can download our data and send to Amazon to upload to the cloud.

Rule of thumb is if it takes more than a week to transfer over the network, use Snowball devices!

If you want to transfer more than 10PB of data (10,000TB) AWS Snowmobile is the better option (an actual truck!!)

Snowcone is the only device in the AWS Snow Family capable of migrating data offline (its a small device), capable of migrating up to 24 TB of data.

#### AWS Snowball usage process
1. Request Snowball device from the AWS Console for delivery
2. Install the snowball client on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship the device back to the correct AWS facility
5. Data will be loaded into an S3 bucket
6. Snowball is completely wiped

### Edge Computing
This is processig data whilst it's being created on an _edge location_, which is basically anywhere without internet that produces data e.g. a truck on the road, ship on the sea, mining station underground etc.

For this we setup a _Snowball Edge_ device to do edge computing, its use cases include preprocess data, machine learing at the edge, and transcoding media streams. Eventually we can ship the device back to AWS if needed.

### AWS OpsHub
Historically to use Snow Family devices you needed a CLI, this was rather difficult so AWS created AWS OpsHub (a software we can install on our machine) to manage your Snow Family device via a graphical interface.

## AWS Storage Gateway
AWS Storage Gateway is a hubrid cloud storage service that gives you on-premise access to virtually unlimited cloud storage. The Storage Gateway provides a bridge bewteen your on-premise data and cloud data in S3, allowing on-premise systems to seamlessly use the cloud and leverage its capabilities. Use cases includ disaster recovery, backup & restore, and tiered storage.

# Databases & Analytics
## AWS RDS (Relational Database Service)
Is a managed database service for databases that use SQL as a query language. It allows you to create databases in the cloud that are managed by AWS. Because RDS is a managed service it gives us the following advantages over deploying our databases on EC2: 
- Database provisioning is automatic, patching of the OS is done by AWS
- Continuous backups and restore options to specific timestamp
- Monitoring dashboards
- Multi AZ setup for disaster recovery
- Scaling capability (vertical and horizontal)
- Storage backed by EBS

### RDS Deployments
#### Read Replicas
- Scale the read workload of your database
- Can create up to 15 Read Replicas
- Data is only written to the main database
#### Multi-AZ
- Failover in case of an AZ outage (high availability)
- Basically a cross AZ replica of a database
- Data is only read/written to the main database
- The failover database is passive (not accessible) unless there is an issue with the main database
- Can only have 1 other AZ as failover
#### Multi-Region (Read Replicas)
- Read Replicas are going to be in a different region to the main database
- Enables applications in other regions to read locally from the Read Replica
- Writes happen cross-region (e.g. main db in eu-west-1 , app in us-east-2 must write from there)
- A disaster recovery strategy in case of regional issues
- Enables better performance for applications we have in other regions (due to having a local Read Replica)

Note there is a replication cost for transferring data accross regions

## Amazon Aurora
Like RDS Aurora is a managed database service that enable you to create __relational databases__ on AWS. Aurora is a proprietary technology from AWS (not open sourced). Aurora supports two kind of database technologies, being PostgreSQL and MySQL. Aurora is cloud optimized and claims 5x perrformance improvement over MySQL on RDS, and over 3x the performance of Postgres on RDS. Aurora storage automatically grows incrementally (increments of 10GB) upt to 128TB. Whilst Aurora costs 20% more than RDS it is more efficient.

## Amazon ElastiCache
Works similarly to RDS with managed relational databases, ElastiCache is used to get managed Redis or Mamcached databases. Caches are __in-memory__ databases with high performance and low latency and helps reduce the load off databases for read intensive workloads. Like RDS, ElastiCache is a managed AWS service.

## DynamoDB
A fully managed and highly available database with replication accros 3 AZs. It is part of the __NoSQL database__ family, meaning it is __not a relational database__. It scales to massive workloads (millions of request per seconds, trillions of rows, 100s of TB of storage) and is a distributed _serverless_ database. It is fast and consistent in its performace and has incredibly low latency retrieval (single-digit millisecond latency). DynamoDB is a key/value database and provides a flexible way of insert data.

### DynamoDB Accelerator (DAX)
Is a fully managed in-memory cache for DynamoDB, provides a 10x performance improvement when accessing your DynamoDB tables, so is better to use this instead of ElastiCache. Its secure, highly available and scalable. Note __DAX is only used for and is well integrated with DynamoDB__, while ElastiCache can be used for other databases.

### Global Tables
Is a feature for DynamoDB that makes a DynamoDB table accessible with low latency in multiple regions. It allows users to read/write to any AWS Region because the DynamoDB table is replicated accross regions making it __Active-Active__ replication.

## Redshift
Is a database that is based on PostgreSQL, but is __not used for OLTP__ (online transaction processing), it's __OLAP (online analytical processing)__ used to do __analytics and data warehousing__. Data isn't continuously loaded, i.e. data is loaded once every hour and is stored in colums rather than rows, making Redshift a __columnar__ storage of data.

## Amazon EMR (Elastic Map Reduce)
EMR helps creating __Hadoop clusters (Big Data)__ to analyze and process vast amounts of data. The clusters can be made of __hundreds of EC2 instances__. Use cases for EMR include data processing, machine learning, web indexing, and big data in general.

## Amazon Athena
A __serverless__ query service to __perform analytics against S3 objects__ that uses standard SQL language to query the files.

## Amazon QuickSight
A serverless machine learning-powered business intelligence service to create interactive dashboards. It is integrated with RDS, Aurora, Athena, Redshift etc.

## DocumentDB
DocumentDB is the AWS-implementation of mongoDB (NoSQL Database)

## Amazon Neptune
Neptune is a fully managed __graph__ database. A popular __graph dataset__ would be a __social network__.

## QLDB
Stands for Quantum Ledger Database, QLDB is a fully managed database, is serverless, highly available and provides replication accross 3 AZs. Note a ledger is a book that __records financial transactions__. QLDB is used to __review history of all the changes made to your application data__ over time. It is an __immutable__ system, which means no entry can be removed or modified. In QLDB there is __no decentralization component__, in accordance with financial regulation rules.

## Amazon Managed Blockchain
Blockchain makes it possible to build applications where multiple parties can execute transactions _without the need to a trusted, central authority__, meaning unlike QLDB there is a __decentralization__ aspect to blockchain. Amazon Managed Blockchain is compatible with the frameworks __Hyperledger Fabric__ and __Ethereum__

## AWS Glue
Managed __extract, transformm and load (ETL)__ service and is fully __serverless__.

## DMS
Stands for __Database Migration Service__. Is a quick and secure way to migrate databases to AWS, is resilient and self-healing. 

# ECS - Elastic Container Service
This is used to launch __Docker containers__ on AWS, you must provision & maintain the infrastructure yourself (EC2 instances created in advanced).

## Fargate
This is also used to launch Docker containers on AWS, however it does not require you to provision the infrastructure (no EC2 instances to set up), so is simpler than ECS and is a serverless offering.

## ECR - Elastic Container Registry
This is a private Docker Registry on AWS, this is where you store your Docker images so they can by run by ECS or Fargate. Think of it as an AWS version of DockerHub (but private of course).

# Serverless
A paradigm in which developers don't have to manage servers anymore. Serverless was pioneered by AWS Lambda but now also includes anything that is managed (so databases, messaging, storage, etc.).

__NOTE: Serverless doesn't mean there are no servers involved, it simply means that you do not manage/provision/see them__

Some serverless services we've encountered so far are Amazon S3, DynamoDB, Fargate.

## AWS Lambda
AWS Lambda is an __event-driven__, serverless computing service that runs code in response to events and automatically manages the computing resources required by that code.

### Advantages over EC2
- No servers to manage - instead we have virtual __functions__
- These functions are limited by time, intended for __shorter execution__ times
- They run __on-demand__, so if we need them they will run, if not they won't
- __Scaling is automated__

With AWS Lambda, you pay per call (requests) and per duration (in increments of 1 ms). Its usually very cheap to run AWS Lambda so it's a very popular way to run serverless applications.

## Amazon API Gateway
Fully managed service for developers to easily creaet, publish, maintain, monitor, and secure APIs in the cloud. Its both __serverless__ and scalable, and supports RESTful APIs and WebSocket APIs.

## AWS Batch
This is a fully managed batch processing service allowing you to do batch processing at __any scale__. It is able to efficiently run 100,000s of computing batch jobs on AWS. Batch will dynamically launch __EC2 instances__ or __Spot Instances__, all that is needede from the user is to submit and scheduler batch jobs and the rest is executed by AWS Batch. Batch jobs are defined as __Docker images__ and run on ECS.

Batch = a job with a start and an end

# Amazon Lightsail
Considered somewhat a standalone service in AWS, with Lightsail you are able to get virtual servers, storage, databases, and networking all in one place. Amazon Lightsail is a simpler alternative to using EC2, RDS, ELB, EBS, etc. It is a great tool for people __with little to no cloud experience__. Has high availability but no auto-scaling.
# Deployments & Managing Infrastructure
## CloudFormation
AWS CloudFormation is an infrastructure as code (IaC) service that allows you to easily model, provision, and manage AWS and third-party resources. CloudFormation does this in a declarative fashion, meaning that the user is simply declare the desired state of your infrastructure (i.e. I want a VPC, I want an internet gateway, I want a subnet, I want a route table, I want a security group, and I want an EC2 instance using that security group running inside this subnet), CloudFormation then spins up the infrastructure for you, in the __right order__, with the __exact configuration__ that you specify.
### CloudFormation Stack Designer
This enables us to see all the resources in our infrastructure, as well as the relationship between the components.
## AWS Cloud Development Kit (CDK)
CDK allows you to define your cloud infrastructure using programming languages such as JavaScript, Python, Java. The code is then compiled into a CloudFormation template (JSON/YAML) which in turn CloudFormation can use to create the infrastructure. Therefore you can deploy infrastructure and application runtime code together because they possibly share the same languages.
## AWS Elastic Beanstalk
Elastic Beanstalk is a managed service for deploying and scaling web applications and services. From a cloud perspective, Beanstalk is __Platform as a Service__, so developers only need to be concerned with the application code.

## AWS CodeDeploy
AWS CodeDeploy is a fully managed deployment service that automates software deployments to any instance, including Amazon EC2 instances and instances running on-premises. CodeDeploy is a __hybrid__ service because it works both for on-prem and cloud servers.

## AWS CodeCommit
A competing product to GitHub, CodeCommit allows developers to store their code in a Git-based repository, making it easy for developers to collaborate with others on code.
Unlike GitHub, AWS CodeCommit is private.

## AWS CodeBuild
A fully managed and serverless service that builds code in the cloud, it compiles source cod, run tests. and produced packages that are ready to be deployed.

## AWS CodePipeline
A fully managed CI/CD (Continuous Integration & Continuous Delivery) service that orchestrates the different steps to have code automatically pushed to prodction. 

## AWS CodeAritfact
CodeArtifact is a secure, scalable, cost-effective artifact management service for software development. This service works with common dependency management tools such as Maven, Gradle, npm, pip, etc. Developers and CodeBuild can retrieve dependencies straight from CodeArtifact.

## AWS CodeStar
CodeStar is a service that provides a __unified UI__ to easily manage software development activities in one place. It provides a quick way to correctly set up CodeCommit, CodePipeline, CodeBuild, CodeDeploy, Elastic Beanstalk, etc.

## AWS Cloud9
AWS Cloud9 is a cloud IDE for writing, running and debugging code. Because it is cloud based, Cloud9 can be used within a web browser, meaning you can work on your projects from anywhere with internet with no setup needed. Cloud9 also allows for code collaboration between developers in real-time (pair programming).

## AWS Systems Manager (SSM)
A __hybrid__ service in AWS that helps you manage your EC2 and on-premises systems at scale. SSM allows you to gain operational insights about the state of your infrastructure. Some of its most important fatures include automatic patching of your servers for enhanced compliance, run commands accross an entire fleet of servers from SSM, and store parameter configuration with the SSM Parameter Store.

We need to install an SSM agent onto all the systems that we control, this is what enables us to run commands, patch and configure our servers.

### SSM Session Manager
This allows us to start a secure shell on our EC2 and on-premises servers without the need for SSH access, bastion hosts, or SSH keys needed.

## AWS OpsWorks
Is a service that runs and manages configuration managament tools such as Chef and Puppet. It is an alternative to AWS SSM and can be used to provision standard AWS resources (EC2 instances, Databases, Load Balancers, etc.)
# AWS Global Applications
We are able to make global applications by leveraging AWS Global Infrastructure. Global applications are appllications thaare dployed in multiple geographies, i.e. in AWS they could be doployed in multiple regions and/or edge locations. The benefits of this includes, decreased latency, for services that have end users all over the globe we can deploy our applications closer to them to decrease latency, providing a better experience. Another benefit is disaster recovery, if an AWS region goes down you can fail-over to another region and have your application still working. A distributed global infrastructure is also harder to attack as it protects you against hackers for example, its difficult for them to attack your applciation if its deployed accross multiple regions.

AWS Global Infrastructure contains regions, for deploying applications and infrastructure, which have several availability zones that are made of multiple data centres, and edge locations (points of presence) for content delivery as close as possible to users.

## Route 53
A managed DNS (Domain Name System), a collection of rules and records which helps clients understand ho to reach a server through URLs.

Most common records in AWS:
- www.google.com -> 12.34.56.78 = A record (IPV4)
- www.google.com -> 2001:0db8:85a3:0000:8a2e:0370:7334 = AAAA IPv6
- search.google.com -> www.google.com = CNAME:hostname to hostname
- example.com -> AWS resource = Alias (ex: ELB, CloudFront, S3, RDS, etc.)

### Routing Policies
__Simple routing policy__ - Use for a single resource that performs a given function for your domain, for example, a web server that serves content for the example.com website. Does not have a health check.

__Weighted routing policy__ - Use to route traffic to multiple resources in proportions that you specify. It is basically a form of load balancing.

__Latency routing policy__ - Use when you have resources in multiple AWS regions and you want to route traffic to the region that provides the best latency. Essentially routes traffic from users to the nearest server.
 to minimize latency.

__Failover routing policy__ - Use when you want to configure active-passive failover. So our DNS will perform a health check on our primary instance and in the case the primary instance fails, traffic will be directed to a failover instance, this helps with disaster recovery.

## AWS CloudFront
CloudFront is a Content Delivery Network (CDN). It improves the read performance by caching the content of your website at different edge locations, this in turn improves user experience (reduced latency). Because content is distributed globally companies are getting DDoS protection, integration with Shield, AWS Web Application Firewall.

### CloudFront Origins
- S3 bucket
- Custom Origin (HTTP)

### S3 Transfer Acceleration
Increases the transfer sppeed of files by transferring them to an AWS edge location which will forward the data to the S3 bucket in the target region.

## AWS Global Accelerator
Improves the availability and performance of global applications by using the AWS global network. 2 Anycast IPs are created for your application and traffic is sent through edge locations. 

## AWS Outposts
AWS Outposts are "server racks" that offers the same AWS infrastructure services, APIs and tools to build your own applications on-premises just as in the cloud. AWS will setup and manage "Outposts Racks" within your on-premises infrastructure and you can satrt leveraging AWS services on-premises.

You are responsible for the Outposts Rack physical security since it is located in your own data centre.

## AWS WaveLength
WaveLength Zones are infrsatructure deployments embedded within the telecommunications providers' datacentres at the edge of the 5G networks. This enables you to deploy AWS services to the edge of the 5G networks.

## AWS Local Zones
Allows you to place compute, storage, database and other selected AWS services closer to your end users to run latency-sensitive applications. The idea is to extend your VPC to more locations, essentially an extension of an AWS Region.

Note not all Regions have Local Zones e.g. Ireland has no Local Zones, but N.Virginia has Local Zones such as Boston.

# Cloud Integrations
When we be begin to deploy multiple applications, we would like them to eventually communicate with one another.

The two patterns of application communication are:
1. Synchronous communications (application to application)
2. Asynchronous/Event based (application to queue to application)

Note synchronous communication between applications can be problematic if there are sudden spikes of traffic, in which case it's better to decouple your applications, and there are few ways we can do this in AWS.

## Amazon SQS (Simple Queue Service)
SQS is a fully managed service and is used to decouple applications and is able to scale seamlessly. By default the queue retains messages for 4 days, there is no limit on how many messages can be in a queue, and messages are deleted after they're read by consumers. It is able to perform with low latency and consumers share the work to read messages and scale horizontally.

## Amazon Kinesis
Amazon Kinesis is a managed service for processing big data in real time. You can use Kinesis data streams to collect and process large streams of data records in real time.

## Amazon SNS (Simple Notification Service)
SNS is a managed service that provides message deliver from publishers to subscribers. Publishers communicate asynchronously with subscribers by sending messages to a topic, which is a logical access point and communication channel.

## Amazon MQ
Amazon MQ is a managed message broker service for Apache ActiveMQ and RabbitMQ that streamlines setup, operation, and management of message brokers on AWS. ActiveMQ and RabbitMQ are on-premises technologies that provide you access to open protocols such as MQTT, ZMQP, STOMP, Openwire, WSS. When migrating to the cloud, instead of re-engineering the application to use SQS and SNS, you can use Amazon MQ.

# Cloud Monitoring
## Amazon CloudWatch
Amazon CloudWatch is a monitoring and management service that provides data and actionable insights for AWS, hybrid, and on-premises applications and infrastructure resources. You can collect and access all your performance and operational data in the form of logs and metrics from a single platform.
### Metrics
CloudWatch provides metrics for every servcie in AWS. A metric is a variable to monitor, for example CPUUtilization. CloudWatch enables you to create a metrics dashboard in order to visualize your metrics.
#### Important metrics for AWS services
__EC2 instances__ - CPUUtilization, Status Checks, Network (not RAM)

__EBS volumes__ - Disk Read/Writes

__S3 buckets__ - BucketSizeBythes, NumberOfObjects, AllRequests

__Billing__ - Total Estimated Charge (only in us-east-1)

__Service limits__ - How much you've been using a service API

__Custom metrics__ - Allows you to push your own metrics

### Alarms
Alarms are used to trigger notifications for any metric. 
### Alarms actions
__Auto Scaling__ - increase or decrease EC2 instances "desired" count

__EC2 Actions__ - stop, terminate, reboot, or recover an EC2 instance

__SNS notifications__ - send a notification into an SNS topic

Alarm States: OK, INSUFFICIENT_DATA, ALARM

### Logs
CloudWatch Logs enables you to centralise the logs from all your systems, applications, and AWS services you use. 

You can use Amazon CloudWatch Logs to monitor, store, and access your log files from:
- ELastic Beanstalk: collection from application
- ECS: Collection from containers
- AWS Lambda: collection from function logs
- CloudTrail based on filter
- CloudWatch log agents: on EC2 machines or on-premises servers
- Route53: Log DNS queries

## Amazon EventBridge
Formerly CloudWatch Events, EventBridge is a serverless service that uses events to connect application components together, making it easier for you to build scalable ebent-driven applications.

## AWS CloudTrail
CloudTrail enables auditing, security monitoring, and operational troubleshooting by tracking user activity and API usage. CloudTrail is enabled by default, a trail can be applied to all regions (default) or a single region.

## AWS X-Ray
Provides visual analysis of our applications, providing a complete view of requests as they travel through the application and filters visual data accross payloads, functions, traces, services, APIs, and more with no-code and low-code motions.

The advantages to AWS X-Ray includes troubleshooting performance, understand dependencies in a microservices architecture, pinpoint service issues, identify users that are impacted, etc.

## Amazon CodeGuru
A ML-powered (Machine Learning) service for automated code reviews and application performance recommendations.

CodeGuru provides two functionalities:
1. CodeGuru Reviewer: Automated code reviews for static code analysis
2. CodeGuru Profiler: Visibility/recommendations about application performance during production

## AWS Health Dashboard
AWS Health Dashboard gives you a personalised view into the performance and availability of the AWS services underlying your AWS resources.

# VPC & Networking
## VPC
Amazon Virtual Private Clud (VPC) is a commercial cloud computing service that provides users a virtual private cloud, by provisioning a logically isolated section of AWS Cloud. Amazon VPC enables you to build a virtual network in the AWS cloud.
### IP Addresses in AWS
There are two kinds of IPs in AWS:

__IPv4__ - _Internet Protocol version 4_:
- Public IPv4 can be used on the internet
- EC2 instances are assigned a new public IP address every time it starts (even if not terminated)
- Private IPv4 can be used on private networks (LAN) such as internal AWS networking
- Private IPv4 is fixed for EC2 instances once created

__Elastic IP__ - allows you to attach a fixed public IPv4 address to an EC2 instance

__IPv6__ - _Internet Protocol version 6_:
- Each IP address is public
- Example: 2001:db4:6666:9999:aaaa:mmmm:nnnn:iiii

## Subnets
A subnet is a range of IP addresses in your VPC. You can launch AWS resources, such as EC2 instances, into a specific subnet. Simply put, subnets allows you to partition your network inside your VPC. Whilst a VPC is a "regional resource" (bound by region), subnets are an AZ resource (bount by availability zones).

## Internet Gateway
An Internet Gateway helps communication between our VPC and the Internet. A **public subnet** has a direct route to an internet gateway. Resources in a public subnet can access the public internet. A **private subnet** does not have a direct route to an internet gateway. Resources in a private subnet require a NAT device to access the public internet.

## NAT Gateway
A NAT Gateway (AWS-managed) and NAT Instances (self-managed) allow instances in your private subnets to access the internet whilst remaining private.

## Peering connections
A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. This allows resources to in either VPC to communicate with each other as if they are within the same network.

## Network Access Control List (NACL)
A firewall which controls traffic from and to subnets. With NACL you can have _ALLOW_ and _DENY_ rules, these only include IP addresses. NACL operates at the subnet level, thus applies to all instances inside the associated subnet.

## Security Groups
A firewall that controls traffic to and from and EC2 instance. Security groups only have _ALLOW_ rules that include IP addresses and other security groups.

## VPC Flow Logs
VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC, so we are able to get VPC flow logs, subnet flow logs, and Elastic Network Interface flow logs. By enabling Flow Logs we are able to monitor & troubleshoot connectivity issues.

## VPC Endpoints
VPC Endpoints allow you to connect to AWS services using a private network instead of the public internet network. This in turn gives you enhanced security and lower latency when accessing AWS services. The two types of VPC Endpoints are __Gateway__ which will connect to S3 and DynamoDB, and the other is __Interface__ which can be used to connect to the rest of AWS services.

## AWS PrivateLink (VPC Endpoint Services)
AWS PrivateLink provides private connectivity between VPCs, supported AWS services, and your own on-premises networks without exposing your traffic to the public internet.
It is the most secure and scalable way to expose a service to numerous VPCs and does not require VPC peering, internet gateway, NAT, etc. In order to do this the service VPC will require a Network Load Balancer, and the customer VPC will require an Elastic Network Interface (ENI).

## Site to Site VPN
A Site to Site VPN enables you to connect your on-prem VPN to AWS, the connection will be automatically encrypted and will go over the public internet. For a Site to Site VPN to be implemented between your on-prem datacentre and your VPC you will need to use a Customer Gateway (CGW) for on-prem, and a Virtual Private Gatweay (VGW) for your VPC.
## Direct Connect (DX)
AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber-optic cable, in other words DX establishes a physical connection between your on-prem datacentre and AWS. The connection is private, secure, and fast and goes over a private network. Compared to a Site-to-Site VPN it takes much longer to set up and is more expensive.

## AWS Client VPN
Allows you to securely connect to your private network in AWS and on-prem using an OpenVPN.

## Transit Gateway
This is a network transit hub that you can use to interconnect your VPCs and on-prem networks. Transit Gateway enables a peering connection bewteen numerous VPCs and on-premises systems. 

# Security & Compliance
## AWS Shared Responsibility Model
The Shared Responsibility Model is a security and compliance framework that outlines the responsibilities of cloud service providers and customers for securing every aspect of the cloud environment.

AWS is responsible for the Security __of__ the Cloud. This includes:
- All the infrastructure provided to you that runs all the AWS services
- Managed services like S2, DynamoDB, etc.

The customer is responsible for Security __in__ the Cloud. This includes:
- For EC2 instance, the customer is responsible for management of the guest OS, firewall & network configuration, IAM permissions
- Encrypting application data

Shared responsibility:
- Patch management
- Configuration management
- Awareness & Training

![](images/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg)

## DDoS Protection
DDos stands for __Distributed Denial-of-Service__, this occurs when multiple systems flood the bandwidth or resources of a targeted system, usually one or more web servers, overwhelming the system to a point where it becomes inaccessible and unresponsive.

## AWS Shield 
AWS Shield is a managed DDoS protection service that safeguards applications running on AWS. There are two tiers of AWS Shield: Standard and Advanced

### Standard
Provides protection against DDoS attacks for your website and applications, and is available for all AWS users at no additional costs. AWS Shield Standard defends against the most common, frequently occurring network and transport layer DDoS attacks that target your website or applications.

### Advanced
Provides 24/7 premium DDoS protection for your website and applications. AWS Shield Advanced is used for higher levels of protection against attacks targeting ypur applications running on EC2, ELB, Amazon CloudFront, AWS Global Accelerator, and Amazon Route 53 resources. In addition to the network and transport layer protections that come with Standard, Shield Advanced provides additional detection and mitigation against large and sophisticated DDoS attacks, near real-time visibility into attacks, and integration with AWS WAF, a web application firewall.

## AWS WAF
AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to CloudFront, and lets you control access to your content. WAF allows you to filter specific requests based on rules. We can deploy WAF on ALB, API Gateway, and CloudFront. We can also define Web ACL, its rules can inclued IP addresses, HTTP headers, HHTP body, or URI strings. Web ACLs protects from common attacks such as SQL injection and Cross-Site Scripting (XSS) and also allows us to block access from certain countries with geo-match. And for DDoS protection we can define rate-base rules (to count occurrences of events).

## Penetration Testing on AWS Cloud
Penetration Testing is when you simulate attacks against your own infrastructure in order to test your infrastructures security. AWS allow customers to carry out security assessments or penetration tests against their AWS infrastucture without prior approval for permitted services such as EC2 instances, NAT Gateways, ELBs, RDS, CloudFront, Lambda, etc.

Some activities when it comes to penetration testing in AWS are prohibited, these include:
- DNS zone waling via Amazon Route 53 Hosted Zones
- DoS, DDoS, not allowed to simulate either
- Port flooding
- Protocol flooding

## Encryption
There are two ways we can encrypt data in AWS, which are encryption _at rest_ and _in transit_. For full time protection, we ideally want our data to be encrypted during both states, for this we leverage __encryption keys__.

### Data at rest
This is data storad or archived on a device (hard disk, RDS instance, S3 Deep Archive, etc.)

### Data in transit (in motion)
This is data being moved from one location to another (transfer from on-prem to AWS, EC2 to DynamoDB, etc.). This means data transferred on the network.

## AWS KMS (Key Management Service)
AWS Key Management Service gives you centralized control over the cryptographic keys used to protect your data. With KMS, AWS manages the encryption keys for us. Some of the objects in AWS we can opt to encrypt include EBS volumes, S3 buckets, Redshoft database, RDS database, EFS drives. Encryption is automatically enabled for CloudTrail Logs, S3 Glacier, Storage Gateway.

## CloudHSM
AWS CloudHSM lets you manage and access your keys on FIPS-validated hardware, protected with customer-owned, single-tenant HSM instances that run in your own Virtual Private Cloud (VPC). With CloudHSM you are entirely responsible for managing your encryption keys.

## AWS Certificate Manager (ACM)
A service that lets you provision, manage, and deploy SSL/TLS Certificates which are used to provide in-flight encryption for websites (HTTPS).

## AWS Secrets Manager
A secrets management service that helps you protect access to your applications, services, and IT resources. This service enables your to easily manage, retrieve, and rotate database credentials, API keys, and other secrets throughout their lifecycles. This service is mostly meant for RDS integration.

## AWS Artifact
AWS Artifact (not really a service but is presented as one in the console), is a portal that provides customers with on-demand access to AWS compliance documentation and AWS agreements. This can be used to support internal audit or compliance within the AWS cloud.

## Amazon GuardDuty
Intelligent Threat discovery to protect your AWS Account. GuardDuty uses Machine Learning algorithms, anomaly detection, and third party data. The input data GuardDuty uses includes CloudTrail Events Logs, VPC Flow Logs, DNS Logs, EKS Audit Logs. We can setup EventBridge rules to be notified of findings. GuardDuty is a very good tool to protect against CryptoCurrency attacks (has a dedicated "finding" for it).

## Amazon Inspector
A service that allows you to carry out automated security assessments. Amazon Inspector can be used to analyse EC2 instances, Container Images pushed to Amacon ECR, and Lambda Functions. Amazon Inspector is integrated with AWS Security Hub and will report findings to it, it will also send findings to Amazon EventBridge.

## Config
AWS Config is a fully managed service that provides you with resource inventory, configuration history, and configuration change notifications to use security and governance. It helps with auditing and recording compliance of your AWS resources.

## Macie
Is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS. Macie helps identify and alert you to sensitive data, such as personally identifiable information(PII).

## AWS Security Hub
The central security tool to manage security accross several AWS accounts and automate security checks. Security Hub collects security data from accross AWS accounts, services, and supported thrid-party partner products and helps you analyse security trends and identify the highest priority security issues.

## Amazon Detective
Amazon Detective makes it easy to analyse, investigate, and quickly identify the root cause of security findings or suspicious activities (using machine learning and graphs). Amazon Detective will automatically collect and process events from VPC Flow Logs, CloudTrail, GuardDuty and create a unified view and produce visualisations with details and context to get to the root cause.

## Root User Privileges
In AWS the Root user is the account owner and is created at the same time the account is created. Root user has complete access to all AWS services and resources, but it is best practice to create an IAM user to perform everyday activities, including administrative tasks. __Lock away your AWS account root user access keys!__

Actions that can only be performed by the root user includes:
- Change account settings (name, emaol address, root user password, root user access keys)
- Close your AWS account
- Restore IAM user permissions
- Change or cancel your AWS support plan
- Register as a seller in the Reserved Instance Marketplace
- Configure and S3 bucket to enable MFA

## AWS IAM Access Analyser
IAM Access Analyser helps you identify the resources in your organisation and accounts, such as S3 buckets or IAM roles, shared externally. IAM Access Analyser allows you to define a __Zone of Trust__, which corresponds to your AWS Account or Organisation, anything from outside the zone of trust that has access to resources within your account or organisation will be reported as findings.

# Machine Learning

## Rekognition
A service that finds objects, people, text, scenes in images and videos using ML. It can perform facial analysis and facial search to do user verification, people counting.

## Transcribe
Automatically converts audio input into text. Amazon Transcribe uses a deep learning process called automatic speech recognition (ASR) to convert speech to text quickly and accurately. Some of Transcribe's features include automatically removing PII using Redaction, and supports Automatic Language Identification for multi-lingual audio.

## Polly 
Amazon Polly is a service that converts text into spoken audio, can be thought of as the reverse of Amazon Transcribe. Amazon Polly uses deep learning technologies to synthesize natural-sounding human speech.

## Translate
A service that performs natural and accurate language translation. Amazon Translate allows you to localise content such as websites and applications for international users, and to easily translate large volumes of text efficiently.

## Lex
Amazon Lex is an AWS service for building conversational interfaces for applications using voice and text. With Amazon Lex, the same conversational engine that powers Amazon Alexa is now available to any developer, enabling you to build sophisticated, natural language chatbots into your new and existing applications.

## Amazon Connect
Amazon Connect is a virtual contact centre that allows you to receive calls, create contact flows, and is cloud-based. Connect can integrate with other Customer Relationship Management systems or AWS service.

## Comprehend
This is a natural language processing (NLP) service that uses machine learning to find insights and relationships in text.

## SageMaker
Amazon SageMaker is a managed service in AWS for developers/data scientist to buuld ML models for predictive analytics applications.

## Forecast
Amazon Forecast is a fully managed service that uses statistical and machine learning algorithms to deliver highly accurate time-series forecasts.

## Kendra
Highly accurate and intelligent search service that allows your users to search unstructired and structured data using natural language processing and advanced search algorithms. It returns specific answers to questions, giving users an experience that's close to interacting with a human expert, and will also learn from user interactions/feedback to promote preferred results (Incremental Learning).

## Personalize
Amazon Personalize is a fully managed ML-service used to build apps with real-time personalised recommendations.

## Textract
Amazon Textract is a ML service that automatically extracts text, handwriting, and data from scanned documents. It goes beyond simple optical character recognition (OCR) to identify, understand, and extract data from forms and tables.

# Account Managaement, Billing & Support

## Organizations
AWS Organization is a global service that allows you to manage multiple AWS accounts, with the main account being the master account, and all other accounts being child accounts.

Cost Benefits:
- Consolidated Billing
- Aggregatd usage
- Pooling of Reserved EC2 instances

With AWS Organizations there is an API available to automate the creation of an AWS account. Organizations also allows you to restrict account privileges using Service Control Policies (SCP).
### Multi Account Strategies
You can create accounts per:
- Department
- Cost centre
- environments (dev/test/production)

These can be created based on regulatory restrictions (using SCP), for better resource isolation (e.g. VPC), to have separate per-account service limits, isolated account for logging.

### Service Control Policies (SCP)
- Whitelist or blacklist IAM actions
- Applied at the OU or Account level
- Does not apply to the Master Account
- SCP is applied to all Users and Roles of the Account, including Root
- The SCP does not affect service-linked roles
- SCP must have an explicit Allow (does not allow anything by default)

### Consolidated Billing
When this is enabled for Organizations, it provides you with the combined usage accross all AWS accounts in the AWS Organization to share the volume priving, reserved instances and savings plan discounts. Thus we are able to get one bill for all AWS accounts in the AWS Organization.

## AWS Control Tower
An easy way to set up and govern a secure and compliant multi-account AWS environment based on best practices. AWS Control Tower runs on top of AWS Organizations, meaning it can automatically set up AWS Organizations to organise accounts and implement SCP.

## Service Catalog
Users that are new to AWS have too many options and may create stacks that are not compliant with the rest of the organization, and some users just want a quick self-service portal to launch a set of authorized products that have been pre-defined by admins. Service Catalog enables organisations to create and manage catalogs of IT services that are approved for AWS, and these services can include everything from virtual machines, servers, databases, and more to complete multi-tier application architectures. Service Catalog allows organizations to centrally manage commonly deployed IT services, and helps organizations achieve consistent governance and meet compliance requirements. End users can quickly deploy only the approved IT services they need, following the constraints set by your organization.

## Pricing Models in AWS
AWS has 4 pricing models:
- Pay as you go - pay for what you use
- Save when you reserve
- Pay less by using more - volume-based discounts
- Pay less as AWS grows
## Free services & free tier in AWS
### Free services
- IAM
- VPC
- Consolidated Billing
- _Elastic Beanstalk_
- _CloudFormation_
- _Auto Scaling Groups_

_Note whilst these services are free you do pay for the resources they create._
### Free tier
https://aws.amazon.com/free/

## Compute Pricing
### EC2
- On-demand instances
- Reserved instances (up to 75% discount compared to On-demand or hourly rate)
- Spot instances (up to 90% discount compared to On-demand or hourly rate)
- Dedicated Host
- Savings plans
### Lambda & ECS
Lambda:
- Pay per call
- Pay per duration

ECS:
- EC2 Launch Type Model: No additional fees, you pay for the resources stored and created in your application

Fargate:
- Fargate Launch Type Model: Pay for vCPU and memory resources allocated to your applications in your containers

## Storage Pricing
### S3
Storage class:
- S3 Standard
- S3 Infrequent Access
- S3 One-Zone IA
- S3 Intelligent Tiering
- S3 Glacier and S3 Glacier Deep Archive

Similar service: EFS (pay per use, has infrequent access & lifecycle rules)

### EBS
- Volume type (based on performance)
- Storage volume in GB per month provisioned
- Snapshots
- IOPS
- Data transfer

## Database Pricing
### RDS
- Per hour billing
- Database characteristics
- Purchase types: On-demand, and Reserved instances (1 or 3 years)
- Additional storage (per GB per month)
- Deployment type (single or multi AZ)
- Data transfer (inbound is free)

## Content Delivery
### CloudFront
- Pricing is deifferent accross different geographic regions
- Aggregated for each edge location, then applied to your bill
- Data Transfer Out (volume discount available)
- Number of HTTP/HTTPS requests

## Savings Plan
Savings Plans is a flexible pricing model that provides savings of up to 72% on your AWS compute usage. Savings Plans offer significant savings over on-demand instances, just like EC2 Reserved instances, in exchange for a commitment to use a specific amount of compute power (measured in $/hour) for a one or three-year period.

The two types of savings plans are:

### EC2 Savings Plan
- Up to 72% discount compared to On-demand
- Commit usage to individual instance familier in a region (e.g. C5 or M5)
- Regardless of AZ, size, OS, or tenancy
### Compute Savings Plan
- Up to 66% discount compared to On-demand
- Regardless of Family, Region, size, OS, tenancy, compute options
- Compute Options: EC2, Fargate, Lambda
### Machine Learning Savings Plan
- Applies to services like SageMaker
- Setup from the AWS Cost Explorer console

## AWS Compute Optimizer
Compute Optimizer is used to reduce costs and improve performance by recommending optimal AWS resources for your workloads. Compute Optimizer analyses the configuration and utilization metrics of your AWS resources and reports whether your resources are optimal, it does this via Machine Learning. Its supported resources includes EC2 instances, ASG, EBS volumes, Lambda functions and can lower your costs by up to 25%.

# Billing and Costing Tools
## Estimating costs in the cloud
### Pricing Calculator
A tool that is used to estimate the cost for your solution architecture.

## Tracking Costs in the Cloud
### Billing Dashboard
A tool that will give you a high level overview of your costs for the month (including forecasts)
### Free Tier Dashboard
Shows usage of all free tier resources for the month.
### Cost Allocation Tags
A tool that we can use to track our AWS costs on a detailed level. There are two types of tags which are AWS generated tags (starts with prefix aws:), and User-defined tags (starts with prefix user:)
### Tagging and Resource Groups
Tags are used for organising resources e.g. EC2 instances, security groups, load balancers, RDS, VPC resources, IAM users, and resources created by CloudFormation. Common tags are: Name, Environment, Team, etc. Tags can be used to create Resource Groups to create, maintain, and view a collection of resources that share common tags, these tags can be managed using the Tag Editor.
### Cost and Usage Reports
This allows you to dive deeper into your AWS costs and usage. The AWS Cost and Usage Report contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, and reservations (e.g. EC2 Reserved Instances).
### Cost Explorer
A tool used to visualise, understand, and manage your AWS costs and usage over time. It allows you to create custom reports that analyse cost and usage data at a high level. With Cost Explorer you can access your optimal savings plan to lower your bill and you can forecast usage up to 12 months based on previous usage.

## Monitoring Costs in the Cloud
### Billing Alarms in CloudWatch
The billing data metric is sored in CloudWatch us-east-1 region only, this metric is for an aggregated worldwide cost i.e. your costs accross all AWS regions. This is intended as a simple alarm in AWS to trigger and notify you incase you cross a certain threshold.

### AWS Budgets
Budgets is a tool you can use to send alarms when your costs or forecasts exceed your defined budget. The 3 types of budgets are Usage, Cost, and Reservation.

### Cost Anomaly Detection
This is a service that cintinuously monitor your cost and usage using ML to detect unusual spends. It learns your unique historic spend patterns to detect one-time cost spike and/or continuous cost increases. If an anomaly is detected it will send you a report with root-cause analysis, you can get notified with individual alerts or daily/weekly summary using SNS.

### AWS Service Quotas
Service Quotas is an AWS service that helps you manage your quotas for many AWS services, from one location. Along with looking up the quota values, you can also request a quota increase from the Service Quotas console.

## Trusted Advisor
A service that provides a high level AWS account assessment. Trusted Advisor will analyse your AWS accounts and provides recommendations on 5 categories:
1. Cost optimization
2. Performance
3. Security
4. Fault tolerance
5. Service limits

### Support Plans
There are __7 core checks__ available to us by default for Basic & Developer Support plan:
- S3 Bucket Permissions
- Security Groups - Specific Ports Unrestricted
- IAM Use
- MFA on Root Account
- EBS Public Snapshots
- RDS Public Snapshots
- Servcie Limits

Then there are __full checks__ for Business & Enterprise Support plan:
- Full checks available on the 5 categories of Trusted Advisor
- Ability to set CloudWatch alarms when reaching limits
- Programmatic Access using AWS Support API

## Support Plans Pricing
There are several support plans available in AWS.
### Basic Support Plan
This plan is free, you get 24/7 access to customer service, documentation, whitepapers, and support forums. For AWS Trusted Advisor we only get access to the 7 core checks. We also have access to the AWS Personal Health Dashboard.
### Developer Support Plan
You get everything from the basic support plan as well as business hours email access to Cloud Support Associates.
### Business Support Plan (24/7)
This is a plan intended to be used if you have production workloads. With regards to Trusted Advisor, this support plan allows you to benefit from the full set of checks and API access. You are also granted 24/7 phone, email, and chat access to Cloud Support Engineers. You can also gain access to Infrastructure Event Management for an additional fee. For the Business Support plan if you have reported cases of your production system being impaired you should expect a response time of less than 4 hours (less than 1 hour if the system is down).
### Enterprise On-Ramp Support Plan (24/7)
Intended to be used uf you have production or business critical workloads. This has everything in the Busiess Support plan as well as access to a pool of Technical Account Managers, a Concierge Support Team for billing and account best practices, and you can get Infrastructure Event Management, Well-Architected & Operations Reviews. In terms of case response times, it is the same as the Business support plan however if a business-critical system is down you can expect a response time of less than 30 minutes.
### Enterprise Support Plan (24/7)
Intended to be used if you have mission critical workloads. This plan has all of the Business Support plan as well some of the other features of On-Ramp, but with a designated TAM, and for a case of a business-critical system being down the response time is less than 15 minutes.

# Advanced Identity
##  Security Token Service (STS)
This is a web service that enables you to request temporary, limited-privilege credentials for users.

## Amazon Cognito
A way to provide identity for your Web and Mobile application users. Instead of creating them as IAM users, you create a user in Cognito.

## Directory Services
AWS Directory Service provides multiple ways to use Microsoft Active Directory (AD) with other AWS services. Directories store information about users, groups, and devices, and administrators use them to manage access to information and resources.

The three flavours of AWS Directory Services are:
#### AWS Managed Microsoft AD
- Create your own AD in AWS, manage users locally, supports MFA
- Establish "trust" connections with your on-prem AD
#### AD Connector
- Directory Gateway (proxy) to rediract to on-ppremise AD, supports MFA
- Users are managed on the on-prem AD
#### Simple AD
- AD-compatible managed directory on AWS
- Cannot be joined with on-prem AD

## IAM Identity Center
The successor to AWS Single Sign-On, this provides one ligin for all your AWS accounts in AWS Organizations.

# Other AWS Servies
## WorkSpaces
Managed Desktop as a Service (DaaS) solution to easily provision Windows or Linux desktops. Great to eliminate management of on-premises Virtual Desktop Infrastructure. WorkSpaces can be deployed in multiple ragions, enabling companies to deploy WorkSpaces closer to their users in order to minimise latency.

## AppStream 2.0
Desktop Appliaction Streaming Service that allows you to stream applications to any computer without acquiring or provisioning infrastructure. The application is delivered from within a web browser.

## IoT Core
Iot (Internet of Things) is the netowkr of internet-connected devices that are able to collect and transfer data. AWS IoT Core allows you to easly connect IoT devices to the AWS Cloud, these devices are able to exchange securely and scalably trillions of messages to billions of devices.

## Elastic Transcoder
Amoazon Elastic Transcoder is used to convert media files stored in S3 into media files in the formats required by consumer playback devices (phones etc...).

## AppSync
AWS AppSync can store and sync data accross mobile and web apps in real-time. This makes use of GraphQL (mobile technology from Facebook).

## Amplify
AWS Amplify is a set of tools and services that helps you develop and deploy scalable full stack web and mobile applications.

## Device Farm
This is a fully-managed service that tests your web and mobile apps againsta desktop browsers, real mobile devices, and tablets. Device Farm will run tests concurrently on multiple devices and has the baility to configure device settings (GPS, language, Wi-Fi, Bluetooth, etc.).

## AWS Backup
A fully-managed service to centrally manage and automate backups accross AWS services, in the cloud, and on-premises. Using this service, you can configure backup policies and monitor activity for your AWS resources in one place.

## Disaster Recovery Strategies
- Backup & Restore (Most cost effective)
- Pilot Light
- Warm Standby
- Multi-Site/Hot-Site (Most expensive)

## AWS Elastic Disaster Recovery (DRS)
Allows you to quickly and easily recover your physical, virtual, and cloud-based servers into AWS.

## DataSync
Allows you to move large amount of data from on-premises to AWS. Can synchronise to S3, EFS, FSx for Windows. Replication tasks can be scheduled hourly, daily, weekly and the replication tasks are incremental after the first full load.

## Application Discovery Service
This service allows you to plan migration projects by gathering information about on-premises data centres. There are two types of migration we can do, the first is Agentless Discovery (AWS Agentless Discovery Connector) that gives you information around VM inventory, configuration, and performance hostory. The second type is Agent-based Discovery (AWS Application Discovery Agent) which gives you more information from within your VMs such as system configuration, system performance, running processes, and details of the notwork connection between systems.

## Application Migration Service (MGN)
This service allows you to use a lift-and-shift solution in order to simplify migrating applications to AWS, essentially converting our physical, virtual, and cloud-based servers to run natively on AWS.

## Fault Injection Simulator (FIS)
This is a fully managed service for running fault inkection experiments on AWS workloads. This is based on Chaos Engineering, which is stressing an application by creating disruptive events then observing how the system responds, and implement improvements.

## Step Functions
This is a way for you to build a serverless visual workflow to orchestrate your Lambda functions. Step Functions can integrate with EC2, ECS, on-prem servers, API Gateway, SQS queues, etc.

## Ground Station
This is a full managed service that lets you control satellite communications, process data, and scale your satellite operations. This provides a global network if satellite ground stations near AWS regions and allows you to download satellite data to your AWS VPC within seconds.

## Pinpoint
Amazon Pinpoint is a scalable two-way marketing communications service supporting email, SMS, push, voice, and un-app messaging. In Amzon Pinpoint you create message templates, delivery schedules, highly-targeted segments, and full campaigns.

# AWS Architecting & Ecosystem
## AWS WhitePapers Well-Architected Framework
The AWS Well-Architected Framework helps you understand the pros and cons of decisions you make while building systems on AWS. By using the Framework you will learn architectural best practices for designing and operating reliable, secure, efficient, cost-effective, and sustainable systems in the cloud.

The framework has 6 pillars, which are:
1. Operational excellence
2. Security
3. Reliability
4. Performance efficiency
5. Cost optimization
6. Sustainability

Information on these pillars can be found in AWS official documentation: https://docs.aws.amazon.com/wellarchitected/latest/framework/the-pillars-of-the-framework.html

## Best Practices of the 6 Pillars
## 1) Operational Excellence
Includes the ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.
### Prepare
To prepare for operational excellence, you have to understand your workloads and their expected behaviors. You will then be able to design them to provide insight to their status and build the procedures to support them.

The best tools for this prectice are:
- CloudFormation
- Config
### Operate
Successful operation of a workload is measured by the achievement of business and customer outcomes. Define expected outcomes, determine how success will be measured, and identify metrics that will be used in those calculations to determine if your workload and operations are successful.

The best tools for this practice are:
- CloudFormation
- Config
- CloudTrail
- CloudWatch
- X-Ray
### Evolve
Learn, share, and continuously improve to sustain operational excellence.

The best tools for this practice are:
- CloudFormation
- CodeBuild
- CodeCommit
- CodeDeploy
- CodePipeline
## 2) Security
The Security pillar encompasses the ability to protect data, systems, and assets to take advantage of cloud technologies to improve your security.
### Identity and Access Management
Identity and access management are key parts of an information security program, ensuring that only authorized and authenticated users and components are able to access your resources, and only in a manner that you intend.

The best tools for this practice are:
- IAM
- AWS-STS
- MFA token
- AWS Organizations
### Detection
You can use detective controls to identify a potential security threat or incident. They are an essential part of governance frameworks and can be used to support a quality process, a legal or compliance obligation, and for threat identification and response efforts.

The best tools for this practice are:
- Config
- CloudTrail
- CloudWatch
### Infrastructure Protection
Infrastructure protection encompasses control methodologies, such as defense in depth, necessary to meet best practices and organizational or regulatory obligations.

The best tools for this practice are:
- Amazon CloudFront
- Amazon VPC
- AWS Shield
- Web Application Firewall (WAF)
- Amazon Inspector
### Data Protection
Before architecting any system, foundational practices that influence security should be in place.

The best tools for this practice are:
- Key Management Service (KMS)
- S3
- Elastic Load Balancing (ELB)
- Amazon EBS
- Amazon RDS
### Incident Response
Even with extremely mature preventive and detective controls, your organization should still put processes in place to respond to and mitigate the potential impact of security incidents.

The best tools for this practice are:
- IAM
- CloudFormation
- Amazon CloudWatch Events
## 3) Reliability
The ability of a workload to perform its intended function correctly and consistently when it’s expected to. This includes the ability to operate and test the workload through its total lifecycle.

### Foundations
Foundational requirements are those whose scope extends beyond a single workload or project. Before architecting any system, foundational requirements that influence reliability should be in place.

The best tools for this practice are:
- IAM
- VPC
- Service Quotas
- Trusted Advisor
### Change Management
Changes to your workload or its environment must be anticipated and accommodated to achieve reliable operation of the workload.

The best tools for this practice are:
- Auto Scaling
- CloudWatch
- CloudTrail
- Config
### Failure Management
In any system of reasonable complexity, it is expected that failures will occur. Reliability requires that your workload be aware of failures as they occur and take action to avoid impact on availability.

The best tools for this practice are:
- Backups
- CloudFormation
- S3
- S3 Glacier
- Route 53
## 4) Performance Efficiency
The Performance Efficiency pillar includes the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.
### Selection
The more effective solution for a particular workload varies, and solutions often combine multiple approaches. Well-architected workloads use multiple solutions and activate different features to improve performance.

The best tools for this practice are:
- Auto Scaling
- AWS Lambda
- Amazon BES
- S3
- Amazon RDS
### Review
Cloud technologies are rapidly evolving and you must verify that workload components are using the latest technologies and approaches to continually improve performance.

The best tools for this practice are:
- Cloudformation
- AWS News Blog
### Monitoring
After you implement your workload, you must monitor its performance so that you can remediate any issues before they impact your customers. Monitoring metrics should be used to raise alarms when thresholds are breached.

The best tools for this practice are:
- CloudWatch
- AWS Lambda
### Tradeoffs
When you architect solutions, think about tradeoffs to validate a more efficient approach. Depending on your situation, you could trade consistency, durability, and space for time or latency, to deliver higher performance.

The best tools for this practice are:
- Amazon RDS
- ElastiCache
- AWS Snowball
- Amazon CloudFront
## 5) Cost Optimization
The ability to run systems to deliver business value at the lowest price point.
### Expenditure Awareness
The best tools for this practice are:
- Budgets
- Cost and Usage Report
- Cost Explorer
- Reserved Instance Reporting
### Cost-Effective Resources
Using the appropriate instances and resources for your workload is key to cost savings.

The best tools for this practice are:
- Spot instances
- Reserved instances
- Amazon S3 Glacier
### Matching Supply and Demand
When you move to the cloud, you pay only for what you need. You can supply resources to match the workload demand at the time they’re needed, this decreases the need for costly and wasteful over provisioning.

The best tools for this practice are:
- Auto Scaling
- AWS Lambda
### Optimizing Over Time
As AWS releases new services and features, it's a best practice to review your existing architectural decisions to verify they continue to be the most cost effective. As your requirements change, be aggressive in decommissioning resources, entire services, and systems that you no longer require.

The best tools for this practice are:
- Trusted Advisor
- Cost and Usage Report
- AWS News Blog
## 6) Sustanability
The Sustainability pillar focuses on environmental impacts, especially energy consumption and efficiency, since they are important levers for architects to inform direct action to reduce resource usage. 
### Alignment to Demand
The way users and applications consume your workloads and other resources can help you identify improvements to meet sustainability goals. Scale infrastructure to continually match demand and verify that you use only the minimum resources required to support your users.

The best tools for this practice are:
- EC2 Auto Scaling
- AWS Lambda
- AWS Fargate


## AWS Well-Architected Tool
A free tool to review your architectures against the 6 pillars of the Well-Architected Framework and adopt architectural best practices.

## AWS Right Sizing
EC2 has many instance types, but choosing the most powerful instance type isn't te best choice, because the cloud is elastic. Right sizing is the process of matching instance types and sizes to your workload performance and capacity requirements at the lowest possible cost. 

_Note: Scaling up is easy so always start small_

It is important to Right Size
- before a Cloud Migration
- continuously after the cloud onboarding process (requirements change over time)

## AWS Ecosystem - Free resources
- AWS Blogs: https://aws.amazon.com/blogs/aws/
- AWS Forums (community): https://forums.aws.amazon.com/index.jspa
- AWS Whitepapers & Guides: https://aws.amazon.com/whitepapers
- AWS Quick Starts: https://aws.amazon.com/quickstart/
- AWS Solutions: https://aws.amazon.com/solutions/

## AWS Marketplace
AWS Marketplace is a digital catalog wth thousands of software listings from independents software vendors (3rd party). Examples of these include custom AMIs, CloudFormation templates, SaaS, Containers. Cost of buying in Marketplace will go to your AWS bill. You can sell your own solutions on the AWS Marketplace and become a Marketplace seller.

## AWS Knowledge Center
This is a web portal that contains the most frequent and common questions and requests.

https://aws.amazon.com/premiumsupport/knowledge-center/

## AWS IQ
AWS IQ is used to help you quickly find professional help for your AWS projects. These 3rd party professionals will be AWS Certified experts that you will engage with and pay for on-demand project work, and this is done through IQ.

The way IQ works for customers is they submit a request with a description of their project, they then review the responses from experts on IQ and select the most suitable for their project, following which the selected expert is given appropriate access to the customer's AWS account and the expert is then paid by the customer per milestone (charges are added to the customer's AWS bill).

For experts, they create a profile on IQ and then connect with customers to work on their projects, they will write a proposal for the customer, then they will gain access to the customer's account if selected, and get paid after milestones are met.

## AWS re:Post
This is an AWS-managed Q&A service offering crowd-sourced, expert-reviewed answers to technical questions about AWS that replaces the original AWS Forums. Questions from AWS Premium Support customers that do not receive a response from the community are passed on to AWS Support engineers. re:Post is not intended to be used for questions that are time-sensitive or involve proprietary information.

## AWS Managed Services (AMS)
Provides infrastructure and appliaction support on AWS. AMS offers a team of AWS experts who manage and operate your infrastructure for security, reliability, and availability.