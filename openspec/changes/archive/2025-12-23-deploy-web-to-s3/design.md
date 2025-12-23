# Design: Web Hosting with S3 and CloudFront

## Context
`shortix-web` is a React SPA built with Vite. It needs to be hosted in a way that is highly available, secure (HTTPS), and supports SPA routing (redirecting 404s to `index.html`).

## Goals
- Host the static assets of `shortix-web` on AWS.
- Provide a public HTTPS endpoint.
- Support SPA routing.

## Decisions

### 1. Storage: S3 Bucket
- **Decision**: Create a private S3 bucket.
- **Rationale**: Best practice is to keep the bucket private and use Origin Access Control (OAC) to allow CloudFront to access it, rather than enabling S3 Website Hosting which requires public access to the bucket.

### 2. Distribution: CloudFront
- **Decision**: Use CloudFront with OAC.
- **Rationale**: Provides HTTPS, edge caching, and a mechanism (Custom Error Responses) to handle SPA routing by mapping 404s to `index.html`.

### 3. Deployment Flow
- **Decision**: Manual sync for now (aligned with current workflow).
- **Steps**:
    1. `npm run build` in `shortix-web`.
    2. `aws s3 sync dist/ s3://<bucket-name> --delete`.
    3. `aws cloudfront create-invalidation --distribution-id <id> --paths "/*"`.

## Infrastructure Details

### `02-persistence-auth.yaml` additions:
- `WebsiteBucket`: `AWS::S3::Bucket` (Private).
- `CloudFrontDistribution`: `AWS::CloudFront::Distribution`.
- `CloudFrontOriginAccessControl`: `AWS::CloudFront::OriginAccessControl`.
- `WebsiteBucketPolicy`: `AWS::S3::BucketPolicy` (Allowing OAC).

## Risks / Trade-offs
- **Cold Cache**: Initial deployments may have brief cache inconsistency until invalidation finishes.
- **Cost**: CloudFront has a free tier but incurs costs under high traffic.
