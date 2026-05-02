# CD to EKS with AWS ECR

This folder contains a full CI/CD flow that builds a Java Maven app, pushes a Docker image to ECR, and deploys it to EKS.

## What this pipeline does

- Builds the Java app from java-maven-app/
- Builds and pushes a Docker image to ECR
- Deploys the new image to EKS
- Commits the version bump to the repo

## Prerequisites

- An existing EKS cluster
- An IAM role that GitHub Actions can assume via OIDC
- An existing ECR repository

## Required GitHub variables

Create repository variables (Settings > Secrets and variables > Actions > Variables):

- AWS_ROLE_ARN: IAM role ARN for GitHub Actions to assume
- AWS_REGION: eu-central-1
- EKS_CLUSTER_NAME: eks-cluster-test
- ECR_REPOSITORY: java-maven-app

## Kubernetes deployment

- Manifests live in CD to cluster - ecr/k8s
- The deployment image is templated at deploy time

## How to run it

- Push changes under CD to cluster - ecr/ or java-maven-app/
- Or run the workflow manually from GitHub Actions
- Workflow file: .github/workflows/deploy-eks-ecr.yml
