# Change: Deploy shortix-web to S3

## Why
Currently, the `shortix-web` frontend only runs in the local development environment. To make the application accessible to users, it must be hosted on a public platform. Following the project's technical specifications, we will use AWS S3 for static website hosting, fronted by AWS CloudFront for HTTPS and performance.

## What Changes
- **Infrastructure (shortix-infra)**:
    - Update `02-persistence-auth.yaml` to include an S3 Bucket for web hosting.
    - Update `02-persistence-auth.yaml` to include a CloudFront Distribution for the website.
- **Deployment**:
    - Add a manual deployment script or instructions to build the frontend and sync artifacts to the new S3 bucket.

## Impact
- **Affected specs**: `deployment`
- **Affected code**: `shortix-infra/02-persistence-auth.yaml`, `shortix-web/` (deployment scripts)
