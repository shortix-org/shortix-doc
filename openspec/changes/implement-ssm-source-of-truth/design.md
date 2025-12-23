# Design: SSM Source of Truth Pattern

## Architecture
We will use AWS Systems Manager (SSM) Parameter Store as the authoritative source for all stack outputs needed by other components.

### SSM Hierarchy
Parameters will follow a consistent naming convention:
`/shortix/${Environment}/${Stack}/${ParameterName}`

| Parameter Key | Purpose | Derived From |
| :--- | :--- | :--- |
| `/shortix/prod/networking/vpc-id` | Foundational VPC | `01-networking` |
| `/shortix/prod/networking/private-subnets` | VPC Subnets | `01-networking` |
| `/shortix/prod/persistence/table-name` | DynamoDB Table | `02-persistence-auth` |
| `/shortix/prod/auth/user-pool-id` | Cognito User Pool | `02-persistence-auth` |
| `/shortix/prod/auth/client-id` | Cognito App Client | `02-persistence-auth` |
| `/shortix/prod/api/url` | API Gateway URL | `03-application` |
| `/shortix/prod/web/bucket-name` | S3 Hosting Bucket | `02-persistence-auth` |
| `/shortix/prod/web/distribution-id` | CloudFront Distribution | `02-persistence-auth` |

## Components

### 1. Infrastructure (CloudFormation)
Each stack will include `AWS::SSM::Parameter` resources for its primary outputs.
Example:
```yaml
UserPoolIdParameter:
  Type: AWS::SSM::Parameter
  Properties:
    Name: /shortix/prod/auth/user-pool-id
    Type: String
    Value: !Ref CognitoUserPool
```

### 2. Synchronization Script (`sync-env.sh`)
A shell script in `shortix-web/scripts/` that:
1. Validates AWS credentials.
2. Executes `aws ssm get-parameters-by-path --path /shortix/prod/ --recursive`.
3. Parses the JSON result.
4. Maps SSM keys to Frontend env names:
   - `/shortix/prod/auth/user-pool-id` -> `VITE_USER_POOL_ID`
   - `/shortix/prod/auth/client-id` -> `VITE_CLIENT_ID`
   - `/shortix/prod/api/url` -> `VITE_API_URL`
5. Overwrites (or creates) the `.env` file.

## Trade-offs
- **Pros**: Zero manual config, versioning support (SSM History), multi-environment support.
- **Cons**: Adds a small amount of complexity to the CFN templates.
