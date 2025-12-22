# Proposal: Add E2E Tests

## Why
While we have unit tests and manual smoke tests, we lack automated verification of the deployed API ("real APIs"). Issues like incorrect handler paths or permission errors in AWS can only be caught by testing the live environment.

## What Changes
-   **New Testing Suite**: A dedicated test suite for End-to-End (E2E) verification.
-   **Automated Scenarios**: Scripts to verify critical flows:
    -   Public: Redirection (302/404).
    -   Protected: Create URL and List URLs (requires Authentication).
-   **Helper Utilities**: Tools to manage test users and authentication tokens programmatically.

## Impact
-   **Reliability**: Increases confidence in deployments.
-   **Capabilities**: Adds `verification` spec.
-   **Code**: New directory `shortix-e2e` (or similar) with test code.
