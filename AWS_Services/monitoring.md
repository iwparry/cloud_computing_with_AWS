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