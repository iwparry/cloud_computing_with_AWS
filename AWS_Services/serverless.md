# Serverless
A paradigm in which developers don't have to manage servers anymore. Serverless was pioneered by AWS Lambda but now also includes anything that is managed (so databases, messaging, storage, etc.).

__NOTE: Serverless doesn't mean there are no servers involved, it simply means that you do not manage/provision/see them__

Some serverless services we've encountered so far are Amazon S3, DynamoDB, Fargate.

## AWS Lambda
AWS Lambda is an __event-driven__, serverless computing service that runs code in response to events and automatically manages the computing resources required by that code.

### Advantages over EC2
- No servers to manage - instead we have virtual __functions__
- These functions are limited by time, intended for __shorter execution__ times
- They run __on-demand__, so if we need them they will run, if not they won't
- __Scaling is automated__

With AWS Lambda, you pay per call (requests) and per duration (in increments of 1 ms). Its usually very cheap to run AWS Lambda so it's a very popular way to run serverless applications.

## Amazon API Gateway
Fully managed service for developers to easily creaet, publish, maintain, monitor, and secure APIs in the cloud. Its both __serverless__ and scalable, and supports RESTful APIs and WebSocket APIs.

## AWS Batch
This is a fully managed batch processing service allowing you to do batch processing at __any scale__. It is able to efficiently run 100,000s of computing batch jobs on AWS. Batch will dynamically launch __EC2 instances__ or __Spot Instances__, all that is needede from the user is to submit and scheduler batch jobs and the rest is executed by AWS Batch. Batch jobs are defined as __Docker images__ and run on ECS.

Batch = a job with a start and an end