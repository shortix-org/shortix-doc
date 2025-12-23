# deployment Specification

## Purpose
TBD - created by archiving change cloud-deployment. Update Purpose after archive.
## Requirements
### Requirement: Deployment Sequence
The infrastructure MUST be deployed in a sequenced manner to ensure data and networking dependencies are resolved.

#### Scenario: Orchestration Order
- **Given** three infrastructure stacks (Networking, Persistence, Application)
- **When** executing the initial deployment
- **Then** Networking must be created first
- **And** Persistence & Auth must be created second
- **And** Application must be created last

### Requirement: Artifact Delivery
Application code MUST be delivered via an immutable artifact storage.

#### Scenario: Code Upload
- **Given** compiled Lambda ZIP files
- **When** the Persistence stack provides an S3 bucket
- **Then** the ZIP files must be uploaded to that bucket before the Application stack is deployed

#### Scenario: Web Assets Upload
- **Given** a built `shortix-web` application
- **When** the Persistence stack provides a Website S3 bucket
- **Then** the application assets must be synced to the bucket
- **And** the CloudFront distribution cache must be invalidated

### Requirement: Environment Verification
Every deployment MUST be followed by a verification of the live endpoint.

#### Scenario: Smoke Test
- **Given** a successfully deployed Application stack
- **When** making a GET request to the root API URL
- **Then** the service must respond with a 200 OK or 404 (if no root path exists) but not a 5xx error.

