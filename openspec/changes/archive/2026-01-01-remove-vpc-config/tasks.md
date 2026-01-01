# Task: Remove VPC Configuration

- [x] Update `03-application.yaml`
    - [x] Remove `VpcConfig` from `CreateUrlFunction`
    - [x] Remove `VpcConfig` from `GetUrlsFunction`
    - [x] Remove `VpcConfig` from `RedirectUrlFunction`
    - [x] Remove `VpcConfig` from `CheckLivenessFunction`
    - [x] Remove `VpcConfig` from `ScanMalwareFunction`
    - [x] Remove `VpcConfig` from `UpdateUrlStatusFunction`
    - [x] Remove `VPCAccess` policy from `LambdaExecutionRole`
    - [x] Cleanup `LambdaSecurityGroup` and unused parameters
- [x] Update `deploy-backend.yml` (Remove VPC params from overrides)
- [x] Deploy and Verify
    - [x] Deploy `application` stack
    - [x] Test `CreateUrl` (expect 201)
    - [x] Check Step Function execution in Console
