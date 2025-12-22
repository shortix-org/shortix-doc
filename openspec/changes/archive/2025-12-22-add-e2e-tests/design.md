# Design: E2E Testing

## Context
We need to verify the system from the outside, treating it as a black box (mostly). The biggest challenge is authenticating automated tests against AWS Cognito.

## Goals
-   Verify "happy path" user journeys.
-   Verify public access.
-   Tests should be runnable locally and in CI.

## Decisions
-   **Test Runner**: `jest` for consistency with the backend.
-   **HTTP Client**: `axios` for simplicity.
-   **Authentication**: Use `@aws-sdk/client-cognito-identity-provider` to perform `INITIATE_AUTH` using a dedicated test user's credentials. This mirrors the frontend's auth flow but programmatically.
-   **Environment**: Target URL and User Credentials will be passed via Environment Variables.

## Risks
-   **Rate Limiting**: Running tests too frequently might trigger AWS throttling or Cognito limits.
-   **Data Cleanup**: Created URLs will persist. We verified the Table has a PK, so we can potentially delete them if we also use DynamoDB SDK, but strict "External E2E" usually avoids direct DB access. *Mitigation*: Accept data accumulation for now or use a dedicated `e2e` stage.
