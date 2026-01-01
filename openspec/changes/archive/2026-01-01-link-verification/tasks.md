# Tasks: link-verification

- [x] Define Step Function Infrastructure
  - [x] Update `shortix-infra/03-application.yaml` to include `AWS::StepFunctions::StateMachine`.
  - [x] Define IAM Roles for Step Functions to invoke Lambdas and update DynamoDB.
- [x] Implement Worker Lambdas in `shortix-lambda`
  - [x] Create `checkLiveness` handler (Head/Get request with retries logic if manual, or rely on SF retry).
  - [x] Create `scanMalware` handler (Mock 30% bad probability).
  - [x] Create `updateUrlStatus` handler (or use direct DynamoDB integration if possible, but Lambda is easier for now).
- [x] Update Entry Point
  - [x] Modify `create_url` Lambda to set `status` = 'PROCESSING'.
  - [x] Trigger Step Function execution from `create_url` (using SDK) OR enable DynamoDB Stream trigger (EventBridge Pipes or Lambda trigger). *Decision: Use SDK trigger for simplicity first.*
- [x] Verification
  - [x] Deploy and create multiple URLs.
  - [x] Verify mixed results (Active/Inactive/Banned) in DynamoDB.
