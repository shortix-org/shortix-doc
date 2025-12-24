# 🚀 Project Specifications: Shortix URL Shortener

## 1. Project Overview
Build a URL shortener system named **Shortix** that allows users to register and log in to manage their links. The system utilizes a Serverless architecture on AWS to optimize costs and scalability.

## 2. Repositories Structure
To maintain separation of concerns, the project will be divided into two separate GitHub repositories:

### 1. `shortix-web`
*   **Purpose**: Contains the Frontend source code.
*   **Technologies**: React, Tailwind, Shadcn UI.
*   **Deploy Target**: AWS S3 + CloudFront.

### 2. `shortix-infra`
*   **Purpose**: Contains the Backend logic (Lambda functions, Layers) and Infrastructure as Code (CloudFormation templates).
*   **Deploy Target**: AWS Lambda, API Gateway, DynamoDB, VPC, etc.

## 3. Tech Stack & Architecture

### Frontend (`shortix-web`)
*   **Framework**: React (TypeScript)
*   **Build Tool**: Vite
*   **Styling**: Tailwind CSS
*   **UI Library**: Shadcn UI (Radix Primitives)
*   **State Management**: React Query (TanStack Query) - for server state management.
*   **Auth**: Amazon Cognito Identity SDK.
*   **Hosting**: AWS S3 (Static Website Hosting) + CloudFront (CDN & SSL).

### Backend & Infrastructure (`shortix-infra`)
*   **Compute**: AWS Lambda (Node.js).
*   **API Management**: Amazon API Gateway (REST API).
*   **Database**: Amazon DynamoDB (On-demand capacity).
*   **Auth Provider**: Amazon Cognito User Pool.
*   **Infrastructure as Code**: AWS CloudFormation.
*   **Network**: AWS VPC (Private Subnets for Lambda, VPC Gateway Endpoints for DynamoDB/S3).

## 4. CloudFormation Strategy
To ensure manageability and logical separation, the infrastructure will be split into 3 distinct CloudFormation templates. These stacks will likely export values (Outputs) to be used by dependent stacks.

### File 1: `01-networking.yaml`
*   **Purpose**: Sets up the foundational network layer.
*   **Resources**:
    *   VPC.
    *   Public & Private Subnets.
    *   Internet Gateway (for public access).
    *   VPC Gateway Endpoints (DynamoDB, S3) to provide private access to AWS services (Free and no NAT required).
*   **Outputs**: `VpcId`, `PrivateSubnetIds`, `PublicSubnetIds`.

### File 2: `02-persistence-auth.yaml`
*   **Purpose**: Sets up stateful resources (Database, Auth, Storage).
*   **Resources**:
    *   **DynamoDB Table**: `UrlShortenerTable`.
    *   **Cognito User Pool**: User directory.
    *   **Cognito User Pool Client**: For the frontend to connect.
    *   **S3 Bucket (Artifacts)**: To store Lambda `.zip` code files.
*   **Outputs**: `DynamoDBTableName`, `UserPoolId`, `UserPoolClientId`, `ArtifactBucketName`.

### File 3: `03-application.yaml`
*   **Purpose**: Sets up the compute and application interface layer.
*   **Resources**:
    *   **IAM Roles**: `LambdaExecutionRole` (referencing policies for DynamoDB/VPC).
    *   **Lambda Layers**: Common dependencies.
    *   **Lambda Functions**: `CreateUrl`, `GetUrls`, `RedirectUrl`.
    *   **API Gateway**: REST API definitions, Resources, Methods, and Cognito Authorizers.
*   **Dependencies**: Requires Outputs from `01-networking.yaml` and `02-persistence-auth.yaml`.

## 5. Functional Requirements

### A. Authentication (Cognito)
1.  **Sign Up**: Email + Password.
2.  **Sign In**: Receive JWT Token (ID Token, Access Token).
3.  **Sign Out**: Revoke local session.

### B. URL Management (Authenticated Users)
*   **Create Short URL**:
    *   **Input**: `original_url` (e.g., https://google.com)
    *   **Process**: Generate `short_code` (e.g., AbCd12), save to DB with `user_id`.
*   **List URLs**:
    *   Show list of URLs created by the current user.
    *   Show click counts (`click_count`).
*   **Delete URL**: Remove item from DB.

### C. Redirection (Public Users)
*   Access `https://api.domain.com/{short_code}`.
*   System finds `original_url` and returns **HTTP 302 Redirect**.
*   Increments `click_count` by 1 (asynchronously).

## 6. Database Design (DynamoDB)

**Table Name**: `UrlShortenerTable`

| Attribute Name | Type | Role | Note |
| :--- | :--- | :--- | :--- |
| `pk` | String | Partition Key | Value: `URL#{short_code}` (optimized for redirect lookup) |
| `sk` | String | Sort Key | Value: `USER#{user_id}` (or empty if not needed for sorting) |
| `gsi1_pk` | String | GSI 1 Partition | Value: `USER#{user_id}` (To list all URLs for a specific user) |
| `original_url` | String | Attribute | The original destination URL |
| `created_at` | String | Attribute | ISO Timestamp |
| `click_count` | Number | Attribute | Number of visits |

## 7. CI/CD Workflows (GitHub Actions)
Deployments are triggered manually (`workflow_dispatch`) to allow control over the target environment.

### Repository 1: `shortix-web` (Frontend Pipeline)
*   **Trigger**: Manual (`workflow_dispatch`).
*   **Inputs**: `environment` (Choice: `dev`, `prod`).
*   **Steps**:
    1.  **Checkout Code**.
    2.  **Setup Node**: Install dependencies (`npm install`).
    3.  **Build**: Run `npm run build` (injects env vars like API URL based on selected environment).
    4.  **Deploy**: Sync `dist/` folder to the target S3 Website Bucket.
    5.  **Invalidate Cache**: Create CloudFront invalidation to serve new content immediately.

### Repository 2: `shortix-infra` (Backend Pipeline)
*   **Trigger**: Manual (`workflow_dispatch`).
*   **Inputs**: `environment` (Choice: `dev`, `prod`).
*   **Steps**:
    1.  **Checkout Code**.
    2.  **Setup Node/Python**: For building Lambda/Layers.
    3.  **Build & Package**:
        *   Install dependencies for Lambda Layers.
        *   Zip Lambda functions code.
        *   Zip Layer code.
    4.  **Upload Artifacts**: Upload the `.zip` files to the S3 Artifact Bucket (created in Stack 2).
    5.  **Deploy Stacks (Sequential)**:
        *   Deploy `01-networking.yaml`.
        *   Deploy `02-persistence-auth.yaml`.
        *   Deploy `03-application.yaml` (Passes S3 keys of the uploaded zips as parameters).
