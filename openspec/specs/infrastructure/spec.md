# infrastructure Specification

## Purpose
TBD - created by archiving change scaffold-infra-stacks. Update Purpose after archive.
## Requirements
### Requirement: Networking Infrastructure
The system SHALL provide a secure networking foundation on AWS.

#### Scenario: VPC Creation
- **WHEN** the networking stack is deployed
- **THEN** a VPC with public and private subnets is created
- **AND** an Internet Gateway is attached for public access
- **AND** a NAT Gateway is configured for private subnet internet access

### Requirement: Persistence and Auth Infrastructure
The system SHALL provision stateful resources for data and identity.

#### Scenario: Database Provisioning
- **WHEN** the persistence stack is deployed
- **THEN** a DynamoDB table `UrlShortenerTable` is created
- **AND** the table uses on-demand capacity

#### Scenario: Identity Provider
- **WHEN** the persistence stack is deployed
- **THEN** a Cognito User Pool is created
- **AND** a User Pool Client is provisioned for the web frontend

### Requirement: Application Infrastructure
The system SHALL provision compute and API resources.

#### Scenario: API Gateway
- **WHEN** the application stack is deployed
- **THEN** a REST API Gateway is created
- **AND** it is integrated with Lambda functions

#### Scenario: Lambda Functions
- **WHEN** the application stack is deployed
- **THEN** Lambda functions for `CreateUrl`, `GetUrls`, and `RedirectUrl` are provisioned

