# Implement Backend Lambda Functions

## Why
The infrastructure scaffolding (`shortix-infra`) defines Lambda functions (`CreateUrl`, `GetUrls`, `RedirectUrl`) but the actual code for these functions does not exist yet. We need to implement the business logic to populate these handlers so the infrastructure can be successfully deployed and functional.

## What
-   Create a new directory `shortix-lambda`.
-   Initialize a TypeScript project for AWS Lambda development.
-   Implement a **Shared Lambda Layer** for common utilities:
    -   Shared DynamoDB Document Client initialization.
    -   Standardized API response formatting (Success/Error) with CORS.
-   Implement the three core functions using the shared layer:
    -   `create_url`: Generates 8-character short codes using `nanoid`, saves to DynamoDB.
    -   `get_urls`: Queries DynamoDB for user's URLs via GSI.
    -   `redirect_url`: Looks up short code and returns 301 Redirect.
-   Implement unit tests for the business logic (Pending).

## Impact
-   **New Component**: `shortix-lambda` (Handlers and Shared Layer).
-   **Infrastructure**: `shortix-infra` stack 03 updated to include the Lambda Layer resource and attach it to all functions.
-   **Dependency**: `shortix-infra` depends on the artifacts (`backend.zip` and `layer.zip`) produced by this component.
