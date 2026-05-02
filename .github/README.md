# GitHub Actions configuration

This folder is required by GitHub Actions. Any workflow placed in .github/workflows is discovered and run by GitHub.

## Workflows in this repo

- deploy-eks.yml: deploys Kubernetes manifests to EKS
- deploy-eks-dockerhub.yml: builds app, pushes image to DockerHub, deploys to EKS
- deploy-eks-ecr.yml: builds app, pushes image to ECR, deploys to EKS

## GitHub authentication

- GitHub automatically provides a short-lived GITHUB_TOKEN during each workflow run.
- That token is used for checkout and for git push when version bumps are committed.
- You can see its permissions in a workflow run under the "Set up job" step.
