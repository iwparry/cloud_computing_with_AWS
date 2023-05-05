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