# Backend Specification Delta

## ADDED Requirements

### Requirement: Automated Link Verification
The system SHALL verify every new shortened URL for liveness and safety asynchronously.

#### Scenario: Newly Created Link
Given a user creates a new short link
Then the link status is initially set to `PENDING`
And a verification workflow is triggered

#### Scenario: Processing Transition
Given a link in `PENDING` status
When the verification workflow starts
Then the link status updates to `PROCESSING`

#### Scenario: Valid Link
Given a link in `PROCESSING` status
When the liveness check returns 200 OK
And the malware scan returns CLEAN
Then the link status is updated to `ACTIVE`

#### Scenario: Dead Link
Given a link in `PROCESSING` status
When the liveness check fails (404 or unreachable)
Then the link status is updated to `INACTIVE`

#### Scenario: Malicious Link
Given a link in `PROCESSING` status
When the malware scan detects a threat (simulated 30% chance)
Then the link status is updated to `BANNED`
And the user account remains active

#### Scenario: System Failure
Given a verification workflow is running
When a system error occurs (e.g. Lambda timeout, unhandled exception)
Then the link status is updated to `FAILED`
