# ECS - Elastic Container Service
This is used to launch __Docker containers__ on AWS, you must provision & maintain the infrastructure yourself (EC2 instances created in advanced).

## Fargate
This is also used to launch Docker containers on AWS, however it does not require you to provision the infrastructure (no EC2 instances to set up), so is simpler than ECS and is a serverless offering.

## ECR - Elastic Container Registry
This is a private Docker Registry on AWS, this is where you store your Docker images so they can by run by ECS or Fargate. Think of it as an AWS version of DockerHub (but private of course).