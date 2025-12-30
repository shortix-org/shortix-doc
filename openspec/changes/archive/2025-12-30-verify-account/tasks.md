# Tasks: verify-account

- [x] Update `AuthContext` in `shortix-web/src/context/AuthContext.tsx`
  - [x] Add `verifyAccount(email: string, code: string)` to `AuthContextType`.
  - [x] Implement `confirmSignUp` using Cognito SDK.
  - [x] (Optional) Add `resendCode(email: string)` method.
- [x] Create Verification UI in `shortix-web`
  - [x] Create `VerifyAccount` component (e.g., `src/pages/VerifyAccount.tsx`).
  - [x] Add route `/verify` in `App.tsx` or router config.
  - [x] Implement form with Email and OTP inputs.
- [x] Integrate Verification Flow
  - [x] Update `SignUp` component to redirect to `/verify` or show verification step upon success.
  - [x] Pass email from SignUp to Verify screen (via state or query param).
- [x] Manual Check
  - [x] Register new user -> Redirect -> Enter Code -> Success.
