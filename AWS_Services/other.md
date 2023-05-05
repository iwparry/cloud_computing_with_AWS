# Other AWS Servies
## WorkSpaces
Managed Desktop as a Service (DaaS) solution to easily provision Windows or Linux desktops. Great to eliminate management of on-premises Virtual Desktop Infrastructure. WorkSpaces can be deployed in multiple ragions, enabling companies to deploy WorkSpaces closer to their users in order to minimise latency.

## AppStream 2.0
Desktop Appliaction Streaming Service that allows you to stream applications to any computer without acquiring or provisioning infrastructure. The application is delivered from within a web browser.

## IoT Core
Iot (Internet of Things) is the netowkr of internet-connected devices that are able to collect and transfer data. AWS IoT Core allows you to easly connect IoT devices to the AWS Cloud, these devices are able to exchange securely and scalably trillions of messages to billions of devices.

## Elastic Transcoder
Amoazon Elastic Transcoder is used to convert media files stored in S3 into media files in the formats required by consumer playback devices (phones etc...).

## AppSync
AWS AppSync can store and sync data accross mobile and web apps in real-time. This makes use of GraphQL (mobile technology from Facebook).

## Amplify
AWS Amplify is a set of tools and services that helps you develop and deploy scalable full stack web and mobile applications.

## Device Farm
This is a fully-managed service that tests your web and mobile apps againsta desktop browsers, real mobile devices, and tablets. Device Farm will run tests concurrently on multiple devices and has the baility to configure device settings (GPS, language, Wi-Fi, Bluetooth, etc.).

## AWS Backup
A fully-managed service to centrally manage and automate backups accross AWS services, in the cloud, and on-premises. Using this service, you can configure backup policies and monitor activity for your AWS resources in one place.

## Disaster Recovery Strategies
- Backup & Restore (Most cost effective)
- Pilot Light
- Warm Standby
- Multi-Site/Hot-Site (Most expensive)

## AWS Elastic Disaster Recovery (DRS)
Allows you to quickly and easily recover your physical, virtual, and cloud-based servers into AWS.

## DataSync
Allows you to move large amount of data from on-premises to AWS. Can synchronise to S3, EFS, FSx for Windows. Replication tasks can be scheduled hourly, daily, weekly and the replication tasks are incremental after the first full load.

## Application Discovery Service
This service allows you to plan migration projects by gathering information about on-premises data centres. There are two types of migration we can do, the first is Agentless Discovery (AWS Agentless Discovery Connector) that gives you information around VM inventory, configuration, and performance hostory. The second type is Agent-based Discovery (AWS Application Discovery Agent) which gives you more information from within your VMs such as system configuration, system performance, running processes, and details of the notwork connection between systems.

## Application Migration Service (MGN)
This service allows you to use a lift-and-shift solution in order to simplify migrating applications to AWS, essentially converting our physical, virtual, and cloud-based servers to run natively on AWS.

## Fault Injection Simulator (FIS)
This is a fully managed service for running fault inkection experiments on AWS workloads. This is based on Chaos Engineering, which is stressing an application by creating disruptive events then observing how the system responds, and implement improvements.

## Step Functions
This is a way for you to build a serverless visual workflow to orchestrate your Lambda functions. Step Functions can integrate with EC2, ECS, on-prem servers, API Gateway, SQS queues, etc.

## Ground Station
This is a full managed service that lets you control satellite communications, process data, and scale your satellite operations. This provides a global network if satellite ground stations near AWS regions and allows you to download satellite data to your AWS VPC within seconds.

## Pinpoint
Amazon Pinpoint is a scalable two-way marketing communications service supporting email, SMS, push, voice, and un-app messaging. In Amzon Pinpoint you create message templates, delivery schedules, highly-targeted segments, and full campaigns.