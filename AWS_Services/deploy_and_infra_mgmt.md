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