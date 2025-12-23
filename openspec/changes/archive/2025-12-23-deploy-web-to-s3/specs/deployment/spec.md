## MODIFIED Requirements
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
