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
Considered somewhat a standalone service in AWS, with Lightsail you are able to get viortual servers, storage, databases, and networking all in one place. Amazon Lightsail is a simpler alternative to using EC2, RDS, ELB, EBS, etc. It is a great tool for people __with little to no cloud experience__. Has high availability but no auto-scaling.
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
