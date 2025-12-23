# Proposal: Implement SSM Source of Truth Pattern

This change introduces the "Source of Truth" pattern using AWS Systems Manager (SSM) Parameter Store. It aims to eliminate manual configuration steps and prevent "configuration drift" by centralizing infrastructure IDs and automating the generation of environment variables.

## Rationale
The recent "User pool client does not exist" error highlighted the risks of manual environment management. By storing critical IDs (Cognito, API, S3) in SSM, we enable:
1. **Automated Sync**: Frontend developer environments can be updated with a single command.
2. **Stack Decoupling**: Application stacks can look up dependencies in SSM rather than requiring manual parameter passing.
3. **Consistency**: Ensures the same IDs are used across development, build, and deployment stages.

## Scope
- **Infrastructure**: Update CloudFormation templates (`01`, `02`, `03`) to write key outputs to AWS SSM Parameter Store.
- **Automation**: Create a `shortix-web/scripts/sync-env.sh` script to fetch parameters and generate the `.env` file.
- **Specifications**: Update `infrastructure` and `deployment` specs to formalize the Source of Truth requirement.

## Impact
- **Developer Experience**: Simplifies local setup and environment switching.
- **Reliability**: Eliminates the most common cause of "integration" bugs in the project.
- **Security**: Parameters are stored in AWS; `.env` files remain git-ignored.
