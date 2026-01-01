# Proposal: remove-vpc-config

## Goal
Remove VPC configuration from all backend Lambda functions to enable direct internet access and resolve Step Functions connectivity timeouts (502 Gateway Errors).

## Context
Currently, Lambda functions (`CreateUrl`, `CheckLiveness`, etc.) are deployed into private subnets within the VPC. However, the VPC lacks a NAT Gateway or VPC Endpoints for Step Functions. This results in:
1.  **Timeouts**: Calls to `StepFunctions.StartExecution` fail because the Lambda cannot reach the AWS service endpoint.
2.  **Liveness Failures**: The `CheckLiveness` function cannot ping public URLs (`google.com`, etc.) because it has no route to the internet.

Since the application does not use private VPC resources (like RDS or ElastiCache), running Lambdas inside the VPC adds complexity (NAT Gateway costs) and latency (ENI creation) without benefit.

## Component Changes

### Backend Infrastructure (`shortix-infra`)
- **`03-application.yaml`**:
    - Remove `VpcConfig` (Subnets, Security Groups) from all `AWS::Lambda::Function` resources.
    - Remove `VPCAccess` managed policy from `LambdaExecutionRole`.
    - Remove `VpcId`, `PrivateSubnetIds` parameters and `LambdaSecurityGroup` resource if they are no longer used by any other resource in the stack.

### Backend Deployment
- **`deploy-backend.yml`**: Review if any `parameter-overrides` need to be removed (though CloudFormation ignores extra parameters if they aren't in the template, it's cleaner to remove).

## Verification
- **Connectivity**: `CreateUrl` should successfully trigger the Step Function execution.
- **Liveness**: `CheckLiveness` should successfully reach public URLs.
- **Response**: API Gateway should return 201 Created instead of 502 Bad Gateway.
