# Proposal: link-verification

## Goal
Implement an automated "Link Doctor" workflow using AWS Step Functions to verify URL health and safety asynchronously after creation.

## Context
Currently, URLs are active immediately upon creation without verification. This can lead to dead links or malicious content being distributed. We want to introduce a verification state machine that runs in the background.

## Component Changes

### Backend (shortix-infra)
- **Infrastructure**:
  - Define a Step Function State Machine in `03-application.yaml`.
  - Add Lambda functions for `CheckLiveness`, `ScanMalware`, and `UpdateUrlStatus`.
  - Update `CreateUrl` Lambda to set initial status to `PENDING` and trigger the Step Function.
  - **Decision**: Use `UpdateUrlStatus` Lambda for all status transitions (SetProcessing, MarkAsFailed) to keep business logic in code.
- **Logic**:
  - **Liveness Check**: Ping URL, retry on failure.
  - **Malware Scan**: Mock function with 30% positive rate.
  - **State Transitions**:
    - Initial: `PENDING`
    - Processing: `PROCESSING`
    - Good: `ACTIVE`
    - Dead: `INACTIVE`
    - Malware: `BANNED`
    - Error: `FAILED`

### API & Database
- Add `status` field to `UrlShortenerTable` (GSI/Projection may be needed if filtering by status).
- DEFAULT status is `PROCESSING`.

## Verification
- Create a URL.
- Observe Step Function execution execution in Console (or mocked via tests).
- Verify Database item updates to correct status based on mock outcome.
