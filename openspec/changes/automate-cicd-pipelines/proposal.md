# Proposal: Automate Deployment with GitHub Actions

This proposal aims to implement fully automated CI/CD pipelines for both the `shortix-web` and `shortix-infra/lambda` repositories.

## Why
Manual deployments (zipping code, uploading to S3, running AWS CLI commands) are error-prone, time-consuming, and difficult to track. Automating these steps ensures consistency, safety, and faster delivery of features.

## What Changes
- **shortix-web:** Create a `.github/workflows/deploy-frontend.yml` to automate build and S3/CloudFront deployment.
- **shortix-infra/lambda:** Create a `.github/workflows/deploy-backend.yml` to automate Lambda build, artifact upload, and CloudFormation stack updates.
- **Project Structure:** Standardize environment variables and secret usage across repos.

## Goals
- Zero manual steps required to deploy code to AWS.
- Consistent build environment using GitHub-hosted runners.
- Automated validation (build/lint) on Pull Requests.
