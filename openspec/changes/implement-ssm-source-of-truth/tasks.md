# Tasks: Implement SSM Source of Truth Pattern

## 1. Infrastructure Updates (shortix-infra)
- [x] 1.1 Update `01-networking.yaml`:
    - Add SSM parameters for `VpcId`, `PublicSubnets`, and `PrivateSubnets`.
- [x] 1.2 Update `02-persistence-auth.yaml`:
    - Add SSM parameters for `DynamoDBTableName`, `UserPoolId`, `UserPoolClientId`, `WebsiteBucketName`, and `CloudFrontDistributionId`.
- [x] 1.3 Update `03-application.yaml`:
    - Add SSM parameter for `ApiUrl`.
- [x] 1.4 Deploy all updated stacks.

## 2. Automation (shortix-web)
- [x] 2.1 Create `shortix-web/scripts/sync-env.sh`.
- [x] 2.2 Add `npm run config:sync` command to `package.json`.
- [x] 2.3 Update documentation in `README.md` (optional follow-up).

## 3. Verification
- [x] 3.1 Run `npm run config:sync`.
- [x] 3.2 Verify `.env` file contents match AWS Console/Outputs.
- [x] 3.3 Verify login functionality continues to work.
