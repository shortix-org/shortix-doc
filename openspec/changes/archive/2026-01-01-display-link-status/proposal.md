# Proposal: display-link-status

## Goal
Display the verification status (`PENDING`, `PROCESSING`, `ACTIVE`, `INACTIVE`, `BANNED`, `FAILED`) of each URL in the `shortix-web` dashboard.

## Context
The backend now performs asynchronous link verification and stores a `status` field in DynamoDB. The frontend `UrlList` component currently ignores this field. Users need visibility into this status to know if their links are ready to use or have been flagged.

## Component Changes

### Frontend (`shortix-web`)
- **`components/UrlList.tsx`**:
    - Update `UrlItem` interface to include `status`.
    - Add a "Status" column to the `Table`.
    - Render the status with appropriate visual cues (Badges/Colors):
        - `ACTIVE` -> Green
        - `PENDING` / `PROCESSING` -> Yellow/Blue
        - `INACTIVE` / `BANNED` / `FAILED` -> Red/Destructive

## Verification
- **Visual Check**: Run the frontend locally and verify the status column appears and shows correct colors for different statuses.
