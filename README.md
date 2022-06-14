# Pipelines

A repository that contains multiple reusable workflows that can be used in GitHub Actions.

## Usage

**Deploy v1.1.0**
```yaml
steps:
- uses: xSpylon/pipelines/.github/workflows/deploy-v1.0.0.yml@main
  secrets:
    ssh_private_key: ${{ secrets.DEPLOYMENT_SSH_PRIVATE_KEY }} # SSH private key in organization/repository secrets
```