# Bank-Microservice-Config

## This repository contains the Centralized Configuration for the Bank Microservices System, including:
##### Accounts Microservice
##### Cards Microservice
##### Loans Microservice

##### The configuration is managed using Spring Cloud Config Server, allowing each microservice to load its settings from this repo based on the active profile (default, qa, prod).


## Profiles Supported
Each microservice has three profiles:

Profile	Purpose

##### default	Local development
##### qa	QA environment & integration testing
##### prod	Production environment

## Microservices load the respective files automatically based on the active profile.

##### For example, for Accounts Service:

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
          
## If using a private repo, configure:
```spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/zsanjay/Bank-Microservice-Config
          username: your-github-username
          password: your-personal-access-token```

          

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

##### Avoid storing sensitive credentials in plain text.

#### Use:
##### HashiCorp Vault
##### AWS Secrets Manager
##### Azure Key Vault
##### Encrypted values ({cipher}) from Spring Cloud
##### Use GitHub PAT tokens for private repo access.

## Features Included

##### Centralized configuration management
##### Profile-specific environment support
##### Dedicated YAML files per microservice
##### Version-controlled configuration
##### Seamless integration with Spring Cloud Config
##### Actuator-based config refresh
##### Infrastructure-ready setup for CI/CD

## Contribution Guidelines

##### Create a branch
##### Update configuration
##### Validate YAML
##### Raise PR
##### Merge only after QA approval
