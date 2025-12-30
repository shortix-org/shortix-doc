# Proposal: verify-account

## Goal
Implement the account verification flow in `shortix-web` to allow users to verify their email address after registration using the confirmation code sent by Amazon Cognito.

## Context
Currently, `shortix-web` supports user registration (Sign Up) and login. However, after registration, users are not prompted to verify their email address, which is a required step for Cognito User Pools when `autoVerify` is not enabled or for security purposes. The `AuthContext` lacks the `confirmSignUp` method, and there is no UI for entering the verification code.

## Component Changes

### Frontend (shortix-web)
- **Shared Functionality**:
  - Update `AuthContext` to expose `verifyAccount(email, code)` which calls `userPool.confirmSignUp`.
- **UI Components**:
  - Create a new `VerifyAccount` page or component.
  - Form with `email` (pre-filled if coming from signup) and `code` fields.
  - Integration with `AuthContext` to submit verification.
- **Routing**:
  - Add route `/verify`.
  - Redirect users to `/verify` after successful signup.

## Verification
- **Manual Verification**:
  - Register a new user.
  - Check email for code (or use console if email sending is mocked/disabled).
  - Enter code in UI.
  - Verify success message and redirection to login/dashboard.
