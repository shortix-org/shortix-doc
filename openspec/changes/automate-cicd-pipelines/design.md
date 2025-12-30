# Design: CI/CD Automation

## Continuous Integration (CI)
Both repositories will have a "Check" workflow triggered on every Pull Request to `main`.
- **Steps:** Checkout, Install dependencies, Lint, Build.

## Continuous Deployment (CD)
Triggered manually (`workflow_dispatch`) to allow controlled releases.

### Backend Pipeline (`shortix-lambda`)
1.  **Checkout Infrastructure:** Checkout the `shortix-infra` repository. The branch should be configurable (defaulting to `main` for production deployments).
2.  **Build:** Run `npm install` and `npm run build`.
3.  **Package:** Create `backend.zip`.
4.  **Upload:** Use `aws s3 cp` to upload artifacts to the S3 bucket defined in the infrastructure.
5.  **Deploy:** Run `aws cloudformation deploy` for Networking, Persistence, and Application stacks sequentially.

### Frontend Pipeline (`shortix-web`)
1.  **Build:** Run `npm install` and `npm run build`.
2.  **Deploy:** Sync `dist/` folder to the S3 Website bucket.
3.  **Invalidate:** Run `aws cloudfront create-invalidation` to refresh the global CDN.

## Security & Secrets
The following secrets MUST be configured in GitHub:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `S3_ARTIFACT_BUCKET` (for backend)
- `S3_WEBSITE_BUCKET` (for frontend)
- `CLOUDFRONT_DISTRIBUTION_ID` (for frontend)
