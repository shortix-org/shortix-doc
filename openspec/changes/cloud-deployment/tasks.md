# Tasks: Cloud Deployment

- [ ] Environment Preparation
    - [ ] Verify AWS CLI access
    - [ ] Ensure `shortix-lambda` build is current
- [ ] Infrastructure Provisioning
    - [ ] Deploy Stack 01: Networking (`01-networking.yaml`)
    - [ ] Deploy Stack 02: Persistence & Auth (`02-persistence-auth.yaml`)
- [ ] Code Packaging & Delivery
    - [ ] Run `npm run package` in `shortix-lambda`
    - [ ] Upload `backend.zip` and `layer.zip` to Artifact S3 Bucket
- [ ] Application Deployment
    - [ ] Deploy Stack 03: Application (`03-application.yaml`)
- [ ] Production Verification
    - [ ] Retrieve API Gateway URL
    - [ ] Perform smoke test on endpoints
