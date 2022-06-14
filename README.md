# Pipelines

A repository that contains multiple reusable workflows that can be used in GitHub Actions.

## Deploy v1.1.0
Automatically deploys a project to a staging or a production environment based on a provided config file.

**GitHub Secret**

Steps: 
1. Generate an SSH private key that will give you access to your server.
2. Create a new GitHub organization/repository secret with a recognizable name such as `DEPLOYMENT_SSH_PRIVATE_KEY`.
3. Paste your SSH private key as the value of the GitHub Secret.


**GitHub Action** 

A GitHub Action should be called in a workflow created under the path `.github/workflows/YOUR_ACTION_NAME`. 

```yaml
steps:
- uses: xSpylon/pipelines/.github/workflows/deploy-v1.0.0.yml@main
  secrets:
    ssh_private_key: ${{ secrets.DEPLOYMENT_SSH_PRIVATE_KEY }} # SSH private key in organization/repository secrets
```

**Pipeline config file** 

A configuration file with the name `pipeline.json` should be created in the root of your project. The following placeholders should be replaced with real data.

```json
{
  "production": {
    "branch": "PRODUCTION_BRANCH_NAME",
    "url": "PRODUCTION_DOMAIN_NAME",
    "host": "PRODUCTION_SSH_IP_ADDRESS",
    "port": "PRODUCTION_SSH_PORT",
    "username": "PRODUCTION_SSH_USERNAME",
    "path": "REMOTE_PATH_TO_DEPLOY_TO"
  },
  "staging": {
    "branch": "STAGING_BRANCH_NAME",
    "url": "STAGING_DOMAIN_NAME",
    "host": "STAGING_SSH_IP_ADDRESS",
    "port": "STAGING_SSH_PORT",
    "username": "STAGING_SSH_USERNAME",
    "path": "REMOTE_PATH_TO_DEPLOY_TO"
  },
  "local": {
    "path": "PATH_TO_DIST"
  }
}
```

Example:
```json
{
  "production": {
    "branch": "main",
    "url": "https://example.com/",
    "host": "12.34.567.890",
    "port": "12345",
    "username": "admin",
    "path": "./"
  },
  "staging": {
    "branch": "dev",
    "url": "https://staging.example.com/",
    "host": "12.34.567.890",
    "port": "67890",
    "username": "admin",
    "path": "./"
  },
  "local": {
    "path": "dist/"
  }
}
```