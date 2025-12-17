# Implement Backend Lambda Functions

## Why
The infrastructure scaffolding (`shortix-infra`) defines Lambda functions (`CreateUrl`, `GetUrls`, `RedirectUrl`) but the actual code for these functions does not exist yet. We need to implement the business logic to populate these handlers so the infrastructure can be successfully deployed and functional.

## What
-   Create a new directory `shortix-lambda` (or `shortix-api`).
-   Initialize a TypeScript project for AWS Lambda development.
-   Implement the three core functions:
    -   `create_url`: Generates short codes, saves to DynamoDB.
    -   `get_urls`: Queries DynamoDB for user's URLs.
    -   `redirect_url`: Looks up short code and returns 301 Redirect.
-   Implement unit tests for the business logic.

## Impact
-   **New Component**: `shortix-lambda`.
-   **Dependency**: `shortix-infra` stack 03 depends on the artifact produced by this component.
