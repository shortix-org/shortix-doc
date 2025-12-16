# Project Context

## Purpose
Shortix is a high-performance URL shortener system built on AWS Serverless architecture.
It allows users to register, log in, create short URLs, and track usage metrics.

## Tech Stack

### Frontend (shortix-web)
- **Core**: TypeScript, React, Vite
- **Styling**: Tailwind CSS, Shadcn UI (Radix Primitives)
- **State**: React Query (TanStack Query)
- **Auth**: AWS Cognito Identity SDK
- **Hosting**: AWS S3 + CloudFront

### Backend (shortix-infra)
- **Runtime**: Node.js (AWS Lambda)
- **API**: Amazon API Gateway (REST)
- **Database**: Amazon DynamoDB (On-demand)
- **Auth**: Amazon Cognito User Pool
- **IaC**: AWS CloudFormation

## Project Conventions

### Architecture Patterns
- **Serverless**: Event-driven architecture using managed AWS services.
- **Repository Structure**: Split into `shortix-web` (Frontend) and `shortix-infra` (Backend).
- **Infrastructure Layering**:
  - `01-networking.yaml`: VPC, Subnets, customizable network.
  - `02-persistence-auth.yaml`: DynamoDB, Cognito, S3 Artifacts.
  - `03-application.yaml`: Lambda, API Gateway.

### Database Strategy (DynamoDB)
- **Table**: `UrlShortenerTable`
- **Patterns**:
  - PK: `URL#{short_code}` (Optimization for Redirects)
  - SK: `USER#{user_id}`
  - GSI1: `USER#{user_id}` (For listing user URLs)

### Deployment & Workflow
- **CI/CD**: GitHub Actions, triggered manually (`workflow_dispatch`).
- **Environments**: `dev` and `prod`.
- **Lambda Layers**: Used for common dependencies.

## Domain Context
- **Short Code**: The unique suffix for a shortened URL.
- **Redirection**: 302 Found response for public access.
- **Click Counting**: Asynchronous increment.

## External Dependencies
- AWS Services (Lambda, API Gateway, DynamoDB, Cognito, S3, CloudFront, VPC)
