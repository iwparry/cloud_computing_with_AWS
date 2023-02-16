# AWS 2-Tier Architecture

A 2-tier architecture is a software architecture that consists of 2 layers, the client tier and the database tier.

## Creating a 2-tier architecture

## Why create a 2-tier architecture?
A 2-tier architecture provides additional to the DBMS (Database Management System) as it isn't exposed directly to the end user.

## Why should we refactor a monolithic architecture into a 2-tier architecture

One of the biggest disadvantages to a monolithic architecture is that everything is bunched into a single component, and thus a single point of failure. We need to refactor into a 2-tier architecture because monolithic systems lack the agility and flexibility that modern businesses require. Also monolithic architectures are not scalable.

## Task: Create a 2-tier architecture with app and DB layers

Requirements:
- App tier deployed - available on public ip on port 3000
- Create a second tier with required dependencies
  - Ubuntu 18.04
  - Mongodb installed
  - Change mongod.conf 0.0.0.0
  - Security group for our DB, port 27017
     - initially allow from anywhere
     - allow only from app instance
- Create environment variable in app instancce with DB endpoint
- Relaunch the app