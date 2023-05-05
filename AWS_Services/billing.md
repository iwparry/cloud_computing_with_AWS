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