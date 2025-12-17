# Tasks: Implement Backend

- [ ] Initialize `shortix-lambda` project (TypeScript, Node 18)
    - [ ] Configure `tsconfig.json` & `package.json`
    - [ ] Install dependencies (`aws-sdk`, `uuid` or `nanoid`, types)
- [ ] Implement `create_url` Handler
    - [ ] Validate input (long URL)
    - [ ] Generate short code (NanoID)
    - [ ] Save to DynamoDB
- [ ] Implement `get_urls` Handler
    - [ ] Query GSI by User ID
    - [ ] Return list of URLs
- [ ] Implement `redirect_url` Handler
    - [ ] Get Item by Short Code
    - [ ] Return 301 response
- [ ] Package/Build Script
    - [ ] Create `build` script to compile TS and zip artifacts for CloudFormation
