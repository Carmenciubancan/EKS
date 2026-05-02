# CD to EKS with DockerHub

This folder contains a full CI/CD flow that builds a Java Maven app, pushes a Docker image to DockerHub, and deploys it to EKS.

## What this pipeline does

- Builds the Java app from java-maven-app/
- Builds and pushes a Docker image to DockerHub
- Deploys the new image to EKS
- Commits the version bump to the repo

## Prerequisites and GitHub setup

See the root README for shared requirements, variables, and secrets.

## Kubernetes deployment

- Manifests live in CD to cluster - dockerhub/k8s
- The deployment image is templated at deploy time

## How to run it

- Push changes under CD to cluster - dockerhub/ or java-maven-app/
- Or run the workflow manually from GitHub Actions
- Workflow file: .github/workflows/deploy-eks-dockerhub.yml
