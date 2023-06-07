# Identity & Access Management (IAM)
In AWS, IAM is an example of a global service, and this service allows you to specify who or what can access services or resoucres within an AWS account and centrally manage permissions that control which AWS resources users can access.  

## Users & Groups
### Root User
When you create an AWS account, you begin with a single sign-in identity that has complete access to all AWS and resources within the account, this is called the __root user__, which is accessed by signing in with the email address and password used to create the account. It is not recommended to use the root user to execute daily tasks, the root user credentials should be safeguarded and only used to perform tasks that can only be performed by the root user.

### Users
In AWS an IAM __user__ is a user within the account (rather than a seperate account). Each user can have its own creadentials to access the AWS Management Console. Generally speaking, users are people within an organization who can be grouped.

### Groups
As the name suggests, in IAM __groups__ are simply groups of users, note that these can only contain Users and not other groups. Within AWS a user does not need to belong to a group, and also a user can belong to multiple groups.

## Permissions & Policies
In AWS we can assign JSON documents called __policies__ to users or groups. The policies define the __permissions__ of the users, i.e. what resource they have access to and what actions they are able to perform on the resource. Policies can be attached to users or groups, as previously mentioned, in the case of a user we either attach a policy directly to the user or we attach a policy to a group, which is inherited by the users contained in that group. Just as a user can belong to multiple groups, a user can have multiple policies assigned to it. In AWS is it recommended to apply the __least privilege principle__.

Here is an example of an IAM policy:
```json
{
    "Version": "2012-10-17",
    "Id": "S3-Account-Permissions",
    "Statement": [
        {
            "Sid": "1",
            "Effect": "Allow",
            "Principal": {
                "AWS": ["arn:aws:iam::123456789012:root"]
            },
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": ["arn:aws:s3:::mybucket/*"]
        }
    ]
}
```
Above we can see how an IAM policy is structured, the policy consists of the following:
- Version: policy language version, this will always by "2012-10-17"
- Id: an identifier for the policy (optional)
- Statement: one or more individual statements (required)

A statement in an IAM policy will consist of:
- Sid: identifier for the statement (optional)
- Effect: whether the statement allows or denies access (Allow, Deny)
- Principal: account/user/role to which this policy is applied to
- Action: list of actions the policy allows/denies
- Resource: list of resources to which the action applies to
- Condition: conditions for when this policy is in effect (optional)

## Password Policy
In AWS IAM allows you to setup a password policy for yoyr users. This policy can inclue minimum password length, requirement for specific character types (like uppercase letters, numbers, etc.), password expiration, and prevent reuse.

## Multi Factor Authentication (MFA)
Another way that IAM enables you to secure your AWS account is MFA which is as the name suggets, adding a stage of authentication when attempting to login to AWS. By setting this up for your root accounts and IAM users this ensures that if the password is somehow stolen, the account is not compromised. There are several MFA options in AWS:
- Virtual MFA devices: Google Authenticator for example. Supports multiple tokens on a single device.
- U2F Security Key: Supports for multiple root and IAM users using a single security key
- Hardware Key Fob MFA Device: Allows you to receive a security token with a hardware device.

## IAM Roles
An IAM __role__ in AWS is essentially a set of permissions assigned to AWS services. There may be cases where we need AWS services to perform actions for us on our behalf, but to do this they require permissions, which we assign to them with IAM roles. Roles can also be used to delegate access to users that don't normally have access to your AWS resources. Roles and users in IAM are similiar except roles are not uniquely associeted with one person.

Roles can be used for the following:
- An IAM user in the same AWS account as the role
- An IAM user in a different AWS accouny than the role
- A web service offered by AWS such as EC2

## IAM Security Tools
These tools within IAM can be useful for audit purposes.

### IAM Credentials Report
This is an account-level report that lists all the account's users and the status of their credentials.
### IAM Access Advisor
This tool is at the user-level and it shows the service permissions granted to a user and when those services were last accessed, this information can be used to revise your policies.

# IAM Guidelines & Best Practices
- __Don't use the root account__ except for AWS account setup, or for performing tasks that can only be performed by the root user
- For every individual that uses the account, __create them their own AWS IAM user__ (i.e. don't create a single user for multiple people)
- Assign __users to groups__, and assign __permissions to groups__
- Create a __strong password policy__
- Use and enforce the use of __MFA__
- Create and use __roles__ for giving permissions to AWS services
- Use __access keys__ for programmatic access (CLI/SDK)
- Audit permissions of your account with the __IAM Credentials Report__
- **Never share IAM users & access keys**