# Proposal: Integrate Web with Backend

## Goal
Connect the `shortix-web` frontend to the `shortix-infra` backend services (Cognito and API Gateway) to enable end-to-end functionality.

## Context
The frontend code contains `AuthContext` and `api` client logic but relies on environment variables (`VITE_USER_POOL_ID`, `VITE_CLIENT_ID`, `VITE_API_URL`) to function. These must be populated with values from the deployed infrastructure.

## Scope
- Configure environment variables.
- Verify user authentication flows (Signup, Login, Logout).
- Verify authenticated API calls (Create URL, List URLs).
- Ensure error handling for auth failures.

## Non-Goals
- UI redesign.
- New backend features.
