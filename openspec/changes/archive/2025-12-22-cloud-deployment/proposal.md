# Proposal: Cloud Deployment

## Why
The backend handlers and infrastructure templates have been implemented and verified locally, but the system is not yet live in AWS. We need a formal process to deploy the three-tier infrastructure, upload artifacts, and verify the production environment.

## What
-   Provision the complete network infrastructure (VPC, Subnets, VPC Gateway Endpoints).
-   Provision persistence and authentication layers (DynamoDB, Cognito).
-   Package and upload Lambda handlers and shared layer.
-   Provision the application layer (Lambda Functions, API Gateway).
-   Establish validation criteria for the live environment.

## Impact
-   **Environment**: The system will be live and accessible via a public API Gateway URL.
-   **Security**: Resources will be protected by VPC networking and Cognito authentication.
-   **Operations**: Establishment of a baseline for future CI/CD and production updates.
