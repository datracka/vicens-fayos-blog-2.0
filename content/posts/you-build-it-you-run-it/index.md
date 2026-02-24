---
id: "YYafCVEOSnuoBh4vG_IihA"
status: "published"
createdAt: "2024-12-16T16:16:45+00:00"
firstPublishedAt: "2024-12-16T16:18:32+00:00"
publishedAt: "2024-12-16T16:18:32+00:00"
updatedAt: "2024-12-16T16:18:31+00:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/dall-e-2024-12-16-17-15-54-a-modern-minimalist-linkedin-post-design-with-a-clean-professional-aesthetic-the-background-is-a-subtle-light-gray-gradient-with-a-central-focus-on.webp"
date: "2024-12-17"
excerpt: "After being tasked with modernizing our CI/CD process, we developed a straightforward approach that significantly improved efficiency. Using a simple \"Hello World\" Next.js app as a reference, I realized this method could be applied across multiple technologies"
slug: "you-build-it-you-run-it"
title: "You build it, you run it"
---

# You build it, you run it

There isn't much to say about the title — you should already have a clear idea of what this is about. Developers should be self sufficient and set all the required data for deploying successfully the app they develop.

In this post, we’ll walk through a workflow that a typical developer might follow.

As an example, we’ll use a `Next.js` project I created as a "hello world" demo. You can find it here: [hello-world-nextjs-k8s-deployment](https://github.com/datracka/hello-world-nextjs-k8s-deployment). We’ll be using GitHub Actions to automate the process. 😊



> \*\*Note:\*\* We assume you have access to a Kubernetes cluster capable of handling and deploying your project. A few months ago, I published some guides on how to set this up. While they may be slightly outdated, they’re still worth checking out. If that doesn't help, you can always turn to LLMs for assistance. Good luck!
>
>



To make this process work, you’ll need to complete the following steps:

1. **Dockerize your project **

    Prepare a Dockerfile for your project to ensure it can be built and run inside a container.

2. **Create a build workflow with GitHub Actions**

    Set up a GitHub Actions workflow that automatically builds the Docker image for every commit to the \`main\` branch and pushes it to Docker Hub.

3. **Create a deployment workflow  **

    Set up another GitHub Actions workflow that runs on demand. This workflow will instruct the Kubernetes cluster to pull the latest Docker image and deploy it.

4. **Coordinate with DevOps  **

    Work with your DevOps team to ensure that the deployment is accessible from the internet.

# Dockerize your Project



In this case, it’s pretty straightforward, and we can go with the "good enough" LLM approach. Let’s use ChatGPT for this https://chatgpt.com/share/67601353-a42c-800f-aee9-805ef2d7b33d



#  Create a Build Workflow



This is part of the CI, so you don't need to do much here. I’ve pasted the one I use. You can either use an LLM to generate it \(although this might result in an updated version of some plugins\) or use Docker plugins, which you can find [here](https://github.com/orgs/docker/repositories) or [here](https://github.com/marketplace).

The file will live in the same repository as the code. Since it’s part of the project, there’s no reason for it to be stored elsewhere.

```bash
name: Build Docker Image

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    env:
      DOCKER_HUB_REPOSITORY: ${{ secrets.DOCKER_HUB_REPOSITORY }}
      IMAGE_NAME: "nextjs-app"
      IMAGE_TAG: ${{ github.sha }}

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_HUB_USERNAME }}
          password: ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          tags: ${{ secrets.DOCKER_HUB_USERNAME }}/${{ env.IMAGE_NAME }}:${{ env.IMAGE_TAG }}

      - name: Logout from Docker Hub
        run: docker logout
```

# Add the secrets

Since we use Docker Hub as our artifact repository, we need to have a repository \(which you will need to create\), a user, and a token. You can find these at \[hub.docker.com\]\(https://hub.docker.com\).

```bash
DOCKER_HUB_REPOSITORY: xxx
DOCKER_HUB_USERNAME: xxx
DOCKER_HUB_ACCESS_TOKEN: xxx
```

# Create Deploy Workflow

Once the image is built and pushed to Docker Hub, we create another workflow to instruct the Kubernetes cluster to download this image and deploy it.

As before, the file will reside in the same repository as the code.

```bash
name: Deploy to Kubernetes on EC2

on:
  workflow_dispatch:
    inputs:
      IMAGE_TAG:
        description: "Tag for the Docker image"
        required: true

jobs:
  deploy:
    runs-on: ubuntu-latest
    env:
      DOCKER_HUB_REPOSITORY: ${{ secrets.DOCKER_HUB_REPOSITORY }}
      IMAGE_NAME: "nextjs-app"
      IMAGE_TAG: ${{ github.event.inputs.IMAGE_TAG }}
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install kubectl
        run: |
          curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
          chmod +x ./kubectl
          sudo mv ./kubectl /usr/local/bin/kubectl

      - name: Configure kubeconfig for the cluster
        run: |
          mkdir -p ~/.kube
          echo "${{ secrets.KUBECONFIG_CONTENT }}" | base64 -d > ~/.kube/config
          chmod 600 ~/.kube/config

      - name: Verify kubectl connection
        run: |
          kubectl config view
          kubectl cluster-info
          kubectl get nodes

      - name: Prepare deployment file
        run: |
          # Print environment variables
          echo "DOCKER_HUB_REPOSITORY: ${{ env.DOCKER_HUB_REPOSITORY }}"
          echo "IMAGE_TAG: ${{ env.IMAGE_TAG }}"
          
          # Print the deployment file before replacement
          echo "Before replacement:"
          cat deployment.yml
          
          # Do the replacement
          sed -i "s|image: PLACEHOLDER_IMAGE|image: ${{ env.DOCKER_HUB_REPOSITORY }}:${{ env.IMAGE_TAG }}|" deployment.yml
          
          # Print the deployment file after replacement
          echo "After replacement:"
          cat deployment.yml
          
          # Verify the exact image string that will be used
          echo "Expected image string: ${{ env.DOCKER_HUB_REPOSITORY }}:${{ env.IMAGE_TAG }}"
          grep "image:" deployment.yml

      # Add this new step to actually apply the deployment
      - name: Apply deployment
        run: |
          kubectl apply -f deployment.yml
          kubectl get deployments
          kubectl get pods
```

You need an additional secret containing the configuration required to use \`kubectl\` remotely.

`secrets.KUBECONFIG\_CONTENT`

You can obtain the content using this LLM chat: \[[chatgpt.com/share/6760237b-8838-800f-8900-ef2d42e4eb86\]\(https://chatgpt.com/share/6760237b-8838-800f-8900-ef2d42e4eb86](chatgpt.com/share/6760237b-8838-800f-8900-ef2d42e4eb86](https://chatgpt.com/share/6760237b-8838-800f-8900-ef2d42e4eb86)\) or, alternatively, you may need to ask your DevOps team or manager for it.

Additionally, you’ll need a Kubernetes \`deployment.yml\` descriptor file in place.

Here’s mine:

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nextjs-app-deployment
  labels:
    app: nextjs-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nextjs-app
  template:
    metadata:
      labels:
        app: nextjs-app
    spec:
      containers:
      - name: nextjs-app-container
        image: PLACEHOLDER_IMAGE # PLACEHOLDER_IMAGE
        resources:
          requests:
            cpu: "0.1"           
            memory: "512Mi"
          limits:
            cpu: "0.1"
            memory: "512Mi"
        ports:
        - containerPort: 3000 
```

You see this `PLACEHOLDER\_IMAGE`, right? This is because, during the CD process, the content of this file will be modified "on the fly" to instruct Kubernetes to pull the correct image. This modification happens in the job mentioned above.

With this in place, you can run this job directly from the \*\*Actions\*\* tab in GitHub, passing the image tag you want Kubernetes to deploy.

And your project will be successfully deployed in the Kubernetes cluster after align with your DevOps.
