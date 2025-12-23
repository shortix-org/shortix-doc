## 1. Infrastructure (shortix-infra)
- [x] 1.1 Add `WebsiteBucket` and `CloudFrontDistribution` resources to `02-persistence-auth.yaml`.
- [x] 1.2 Export `WebsiteBucketName` and `CloudFrontDistributionId`.
- [x] 1.3 Deploy updated `shortix-persistence-auth` stack.

## 2. Deployment Script (shortix-web)
- [x] 2.1 Create `shortix-web/deploy.sh` script to:
    - Build the React application (`npm run build`).
    - Sync the `dist/` folder to the `WebsiteBucket`.
    - Invalidate the CloudFront cache.
- [x] 2.2 Add `npm run deploy` script to `shortix-web/package.json`.

## 3. Verification
- [x] 3.1 Run `npm run deploy`.
- [x] 3.2 Access the application via the CloudFront URL.
- [x] 3.3 Verify SPA routing (refreshing on a sub-path like `/login`).
