# Change: Scaffold Infrastructure Stacks

## Why
The project requires a Serverless infrastructure on AWS to host the Shortix URL shortener. Currently, the `shortix-infra` repository is empty. We need to establish the foundational CloudFormation templates to enable deployment of networking, persistence, and application layers.

## What Changes
- Create `shortix-infra/01-networking.yaml` (VPC, Subnets, Internet Gateway)
- Create `shortix-infra/02-persistence-auth.yaml` (DynamoDB, Cognito, S3 Artifacts)
- Create `shortix-infra/03-application.yaml` (Lambda, API Gateway, IAM Roles)

## Impact
- **Affected Specs**: `infrastructure` (New capability)
- **Affected Code**: `shortix-infra` (New CloudFormation templates)
