# Change: Add Shortix Web Frontend

## Why
Currently, the Shortix project has the backend infrastructure defined (`shortix-infra`) but lacks a user interface. To allow users to register, log in, and manage their short URLs, we need to build a web application.

## What Changes
- Create a new directory `shortix-web` at the project root.
- Initialize a React application using Vite and TypeScript.
- Configure Tailwind CSS and Shadcn UI (Radix Primitives) for styling.
- Implement Authentication pages (Sign Up, Sign In) using AWS Cognito.
- Implement Dashboard pages to listing and creating URLs using the backend API.

## Impact
- **Affected Specs**: `frontend` (New capability).
- **Affected Code**: `shortix-web` (New codebase).
- **Dependencies**: Depends on `infrastructure` for `UserPoolId`, `UserPoolClientId`, and `ApiUrl`.
