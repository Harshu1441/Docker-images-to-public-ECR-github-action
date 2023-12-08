# Docker-images-to-public-ECR-github-action

This GitHub Actions workflow automates the process of building a Docker image and pushing it to Amazon Elastic Container Registry (ECR) when changes are pushed to the specified branch.
Workflow Triggers

The workflow is triggered on each push to the main branch.

yaml

on:
  push:
    branches:
      - main

Workflow Jobs
Build, Tag, and Push

This job runs on a self-hosted runner and consists of the following steps:

    Checkout Repository:
        Uses the official GitHub Actions action to checkout the repository.

    yaml

- name: Checkout repository
  uses: actions/checkout@v2

Login to Amazon ECR:

    Uses the aws-actions/amazon-ecr-login action to authenticate with the specified Amazon ECR registry.

yaml

- name: Login to Amazon ECR
  id: login-ecr
  uses: aws-actions/amazon-ecr-login@v2
  with:
    mask-password: 'true'

Change Directory:

    Navigates to the specified path inside the repository.

yaml

- name: path
  run: |
    cd --path-to-the-repository-inside-work-dir--

Build Docker Image:

    Builds a Docker image using the specified Dockerfile and tags it with the provided ECR repository URL.

yaml

- name: Build Image
  run: |
    export v=--public-ecr-repo-url--
    docker buildx build -t $v -f dockerfile .

Push Docker Image:

    Pushes the built Docker image to the specified ECR repository.

yaml

    - name: Push Image
      run: |
        export v=--public-ecr-repo-url--
        docker push $v:latest

Note: Ensure that you replace placeholders such as --path-to-the-repository-inside-work-dir-- and --public-ecr-repo-url-- with the actual values relevant to your project.

Feel free to customize this GitHub Actions workflow according to your specific requirements and project structure.