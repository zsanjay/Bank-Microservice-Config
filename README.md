# Bank-Microservice-Config

## This repository contains the Centralized Configuration for the Bank Microservices System, including:
### Accounts Microservice
### Cards Microservice
### Loans Microservice

## The configuration is managed using Spring Cloud Config Server, allowing each microservice to load its settings from this repo based on the active profile (default, qa, prod).

## Repository Structure

## Bank-Microservice-Config/
│
├── accounts.yml
├── accounts-qa.yml
├── accounts-prod.yml
│
├── cards.yml
├── cards-qa.yml
├── cards-prod.yml
│
├── loans.yml
├── loans-qa.yml
├── loans-prod.yml
│
└── application.yml

## Profiles Supported
Each microservice has three profiles:

Profile	Purpose

### default	Local development
### qa	QA environment & integration testing
### prod	Production environment

## Microservices load the respective files automatically based on the active profile.

How Microservices Load Configurations
Spring Cloud Config uses naming conventions like:
<application-name>-<profile>.yml
<application-name>.yml


### For example, for Accounts Service:

default → accounts.yml
qa → accounts-qa.yml
prod → accounts-prod.yml

Your microservice must set:
spring:
  application:
    name: accounts
  profiles:
    active: qa
    
## Running via Config Server
Your Config Server should point to this Git repo:
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/zsanjay/Bank-Microservice-Config
          
### If using a private repo, configure:
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/zsanjay/Bank-Microservice-Config
          username: your-username
          password: your-PAT-token
          

## How to Refresh Config Changes
After updating config files, refresh microservices using:
POST http://<service-host>/actuator/refresh
Ensure:
management:
  endpoints:
    web:
      exposure:
        include: "*"
        
## Security Best Practices
Do NOT store secrets in plain text.
Use:
Vault
AWS Secrets Manager
Azure Key Vault
KMS encrypted values ({cipher}) if using Spring Cloud Config + Encryption
Use a PAT (Personal Access Token) if Config Server accesses this private repository.

## Features Included
✔ Centralized configuration management
✔ Profile-specific configuration
✔ Microservice-wise YAML files
✔ Version-controlled environment properties
✔ Auto-refresh support using Spring Actuator
✔ Easy integration with Spring Cloud Config Server

## Contribution Guidelines
Create a branch
Update configuration
Validate YAML
Raise PR
Merge only after QA approval
