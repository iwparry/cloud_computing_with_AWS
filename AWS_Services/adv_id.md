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
The successor to AWS Single Sign-On, this provides one login for all your AWS accounts in AWS Organizations.
