# Frontend Specification Delta

## ADDED Requirements

### Requirement: URL Status Visibility
The system SHALL display the verification status of each URL in the user's dashboard.

#### Scenario: Display Status Column
Given the user is viewing their list of URLs
When the list is rendered
Then it should include a "Status" column
And the status values (ACTIVE, PENDING, BANNED, etc.) should be visible
