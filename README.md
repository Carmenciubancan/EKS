# EKS CI/CD demo repo

This repo contains three GitHub Actions pipelines that deploy to the same EKS cluster:

- Simple CD (apply manifests only) in CD to cluster
- Full CI/CD with DockerHub in CD to cluster - dockerhub
- Full CI/CD with AWS ECR in CD to cluster - ecr

## Quick start

1) Ensure the EKS cluster exists and your IAM role has Kubernetes access.
2) Configure repo variables and secrets in GitHub.
3) Trigger a workflow by pushing changes in the relevant folder or running it manually.

## Pipelines

### 1) CD to cluster (manifests only)

- Workflow: .github/workflows/deploy-eks.yml
- Deploys manifests from CD to cluster/k8s
- Trigger: push changes under CD to cluster/ or manual run

### 2) CI/CD to EKS with DockerHub

- Workflow: .github/workflows/deploy-eks-dockerhub.yml
- Builds the Java app, pushes Docker image to DockerHub, deploys to EKS
- Trigger: push changes under CD to cluster - dockerhub/ or java-maven-app/ or manual run

### 3) CI/CD to EKS with AWS ECR

- Workflow: .github/workflows/deploy-eks-ecr.yml
- Builds the Java app, pushes Docker image to ECR, deploys to EKS
- Trigger: push changes under CD to cluster - ecr/ or java-maven-app/ or manual run

## Required GitHub variables (for all pipelines)

Set repository variables in Settings > Secrets and variables > Actions > Variables:

- AWS_ROLE_ARN: IAM role ARN for GitHub Actions (OIDC)
- AWS_REGION: eu-central-1
- EKS_CLUSTER_NAME: eks-cluster-test

## Additional variables and secrets

DockerHub pipeline:
- Variable: DOCKERHUB_IMAGE (example: dockerhub-user/java-maven-app)
- Secrets: DOCKERHUB_USERNAME, DOCKERHUB_TOKEN

ECR pipeline:
- Variable: ECR_REPOSITORY (example: java-maven-app)

## Where the app lives

The Java Maven app is stored in this repo at java-maven-app/. Workflows build it from there.

## GitHub Actions authentication

- GitHub automatically provides a short-lived GITHUB_TOKEN for each workflow run.
- The workflow uses this token for checkout and optional git push (version bump).

## EKS access requirement

The IAM role used by GitHub Actions must be mapped to Kubernetes permissions in the cluster.
