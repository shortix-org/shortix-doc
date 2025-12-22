# Tasks: Cloud Deployment

- [x] Environment Preparation
    - [x] Verify AWS CLI access
    - [x] Ensure `shortix-lambda` build is current
- [x] Infrastructure Provisioning
    - [x] Deploy Stack 01: Networking (`01-networking.yaml`)
    - [x] Deploy Stack 02: Persistence & Auth (`02-persistence-auth.yaml`)
- [x] Code Packaging & Delivery
    - [x] Run `npm run package` in `shortix-lambda`
    - [x] Upload `backend.zip` and `layer.zip` to Artifact S3 Bucket
- [x] Application Deployment
    - [x] Deploy Stack 03: Application (`03-application.yaml`)
- [x] Production Verification
    - [x] Retrieve API Gateway URL
    - [x] Perform smoke test on endpoints
