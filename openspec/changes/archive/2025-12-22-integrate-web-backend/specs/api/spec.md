# API Integration Requirements

## ADDED Requirements

### Requirement: Authenticated API Requests
All API requests from the frontend to protected endpoints SHALL include a valid authentication token.

#### Scenario: ID Token Injection
Given an authenticated user with a valid session
When the frontend makes an API request
Then the `Authorization` header must contain the ID Token
