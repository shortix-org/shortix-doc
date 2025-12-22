## ADDED Requirements
### Requirement: Automated E2E Verification
The system SHALL support automated end-to-end testing against the deployed API to verify critical functionality.

#### Scenario: Public Access
- **Given** the API Gateway URL
- **When** a user requests a non-existent short code
- **Then** the system returns a 404 error

#### Scenario: Authenticated Creation
- **Given** a valid authentication token for a test user
- **When** the user POSTs to `/urls` with a valid long URL
- **Then** the system returns a 201 Created status and a new short code
