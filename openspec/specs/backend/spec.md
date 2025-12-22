# backend Specification

## Purpose
TBD - created by archiving change implement-backend. Update Purpose after archive.
## Requirements
### Requirement: URL Shortening
The system SHALL provide a function `create_url` that accepts a JSON object with a `url` field, validates the URL, generates a unique short code, persists the mapping to DynamoDB, and returns the short code and metadata.

#### Scenario: Successful URL Creation
Given a valid long URL "https://google.com" passed to `create_url`.
When the function is invoked with an authenticated user context.
Then it should generate a short code (e.g., "abc1234").
And it should save the mapping to `UrlShortenerTable` with `pk=URL#abc1234`.
And it should return the short code and metadata.

### Requirement: URL Retrieval
The system SHALL provide a function `get_urls` that queries the `UserUrlsIndex` in DynamoDB by the authenticated user's ID and returns a list of URL objects sorted by creation time.

#### Scenario: List User URLs
Given a user has created 5 URLs.
When `get_urls` is invoked with the user's authentication token.
Then it should query DynamoDB `UserUrlsIndex` for `gsi1_pk=USER#{user_id}`.
And it should return a list of 5 URL objects sorted by creation time.

### Requirement: URL Redirection
The system SHALL provide a function `redirect_url` that accepts a `short_code`, retrieves the original URL from DynamoDB, and returns an HTTP 301 Redirect response, or an HTTP 404 if the code is not found.

#### Scenario: Redirect Existing URL
Given a short code "abc1234" exists in DynamoDB mapping to "https://google.com".
When `redirect_url` is invoked with `short_code="abc1234"`.
Then it should return a 301 Permanent Redirect to "https://google.com".

#### Scenario: Redirect Non-Existent URL
Given a short code "xyz9999" does not exist in DynamoDB.
When `redirect_url` is invoked with `short_code="xyz9999"`.
Then it should return a 404 Not Found response.

