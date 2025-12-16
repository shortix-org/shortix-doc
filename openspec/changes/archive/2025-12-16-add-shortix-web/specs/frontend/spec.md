## ADDED Requirements

### Requirement: Web Application Stack
The system SHALL provide a web interface built with modern technologies.

#### Scenario: Tech Stack
- **WHEN** the application is initialized
- **THEN** it must use React with TypeScript
- **AND** it must use Vite as the build tool
- **AND** it must use Tailwind CSS for styling

### Requirement: User Authentication Interface
The system SHALL provide screens for users to manage their identity.

#### Scenario: Sign Up
- **WHEN** a visitor accesses the registration page
- **THEN** they can enter email and password
- **AND** submit to create a new account in Cognito

#### Scenario: Sign In
- **WHEN** a user enters valid credentials
- **THEN** they are redirected to the dashboard
- **AND** their session is persisted

### Requirement: URL Management Interface
The system SHALL provide a dashboard for managing short URLs.

#### Scenario: Create URL
- **WHEN** a logged-in user submits a long URL
- **THEN** the system calls the API to generate a short code
- **AND** displays the new short URL to the user

#### Scenario: List URLs
- **WHEN** a logged-in user views the dashboard
- **THEN** they see a list of their created URLs
- **AND** can see the click count for each
