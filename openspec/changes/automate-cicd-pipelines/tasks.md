# Tasks: Automate CI/CD Pipelines

- [x] Backend Pipeline [x]
    - [x] Create `.github/workflows/deploy-backend.yml` in `shortix-lambda`
    - [x] Implement multi-repo checkout for `shortix-infra` with configurable branch
    - [x] Add deployment script/command to `package.json` for easier pipeline usage
- [x] Frontend Pipeline [x]
    - [x] Create `.github/workflows/deploy-frontend.yml` in `shortix-web`
- [x] Documentation [x]
    - [x] Update READMEs with instructions for setting up GitHub Secrets
    - [x] Update `task.md` to reflect the new "Pro" way of deploying
- [x] Verification [x]
    - [x] Run a manual workflow trigger for Backend
    - [x] Run a manual workflow trigger for Frontend
    - [x] Verify the app is live and functional
