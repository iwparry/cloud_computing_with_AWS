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