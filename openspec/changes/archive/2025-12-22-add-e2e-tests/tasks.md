# Tasks: Add E2E Tests

- [x] 1. Setup
    - [x] 1.1 Create `shortix-e2e` directory and initialize TypeScript project
    - [x] 1.2 Install dependencies (`jest`, `axios`, `dotenv`, `@aws-sdk/client-cognito-identity-provider`)
    - [x] 1.3 Configure `jest` and environment variables (`.env`)
- [x] 2. Implementation
    - [x] 2.1 Implement `TestAuth` helper to authenticate a test user against Cognito
    - [x] 2.2 Implement `Basic Flows` test (Public 404, Redirect)
    - [x] 2.3 Implement `User Flows` test (Create URL, Get URLs)
- [x] 3. integration
    - [x] 3.1 Run suite against the deployed `dev` or `prod` environment
