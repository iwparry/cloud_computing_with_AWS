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