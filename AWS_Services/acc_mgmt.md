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