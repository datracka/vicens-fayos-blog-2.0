---
id: "aF-0FIFYT5CDz1esq297xQ"
status: "published"
createdAt: "2024-07-11T09:33:48+01:00"
firstPublishedAt: "2024-07-11T09:33:50+01:00"
publishedAt: "2024-07-11T09:41:43+01:00"
updatedAt: "2024-07-11T09:41:42+01:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/devops_ci.webp"
date: "2024-07-11"
excerpt: "Continuous integration from the software developer's side.\""
slug: "devops-for-sw-devs-continuous-integration"
title: "DevOps for SW Devs: Continuous Integration"
---

# DevOps for SW Devs: Continuous Integration

## What, Why, and When Continuous Integration \(CI\)

Let's start from the beginning: **What is CI?**

As a developer, you need to build the app locally to test the work you are doing. Therefore, you build your application on demand.

**CI is when the application you are developing is built automatically.**

<u>Why do that?</u> Just keep reading... 🙂

But first, as a reminder, what do we understand as a "build"? Well,

- For a Frontend Application, it's having your JS files transpiled/bundled ready to be added to a Web Server as assets.
- For Java applications, it's having the bytecode as a Jar or War ready to run in a JVM.
- For other common server-side languages like PHP, Python, NodeJS, or Ruby, it's having the source code folder \+ dependencies packaged in the dedicated folder in the web server runtime, ready to be interpreted and executed on demand.

As you can see, there are multiple cases, each requiring its own steps for building and later deploying it, making the whole process very manual and specific to each use case.

> There is a difference between building for development and building for deployment because you have different needs. For development, you want to spin off a server locally and have hot module replacement, whereas for production, you want everything packaged and optimized as much as possible.
>
>

Nice, but each tech stack has its own rules for how it should be built... What if we had a way to standardize this process not by standardizing the build itself but by ensuring that these different cases don't affect later steps \(thinking in Continuous Deployment\)?

Is then when **containers** come into play. Regardless of how the application needs to be built, the final output is a container/box encapsulating all this logic and a common API able to manage them.

It is a way to abstract what an App is into a standard container that can later be managed by other professionals \(Hi DevOps!\) without needing to delve too much into what's inside.

<u>That's why</u> Containers \(Docker\) and Kubernetes \(as a Container Orchestrator\) gained popularity in recent years.

Now, we are only missing **WHEN** this automation should happen.

Well, <u>continuously</u>. 😀 It could even be for every micro code change!

But we have to maintain a user-centric perspective, so as a commonly accepted best practice, a new build is triggered every time a code change potentially becomes a new feature for the end user.

And since this is usually related to a PR merge in the branch to be deployed to an environment, we associate building an image with merging a PR into a branch \(main/staging/review/test, you name it\).

> I assume you  have a clear understanding of what a branch and a CVS are. If not... well, go to Google / ChatGPT.
>
>

I hope this explanation helped contextualize  what we are going to do now as a hands-on exercise.

## How to do Continuous Integration



As mentioned, if you want to do CI based on containers, the very first thing you have to do is to wrap your application in a container.

Our App is a simple Rest HelloWorld Java App. You can clone it from \[here\] \(https://github.com/datracka/finance-api\).

For building a container image, you need:

- Having \[Docker\]\(https://www.docker.com/\) installed on your machine.
- Having a Dockerfile like this. In our case, it is tailored for a Java App:

```bash
# First stage: build the application

FROM openjdk:17-jdk-slim as builder
WORKDIR /app
COPY . .
RUN ./mvnw clean package

# Second stage: run the application

FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=builder /app/target/api-1.0.0.jar /app/api-1.0.0.jar
EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app/api-1.0.0.jar"]
```

- Then you can build an image and run the container locally.

> For example, \`docker build -t my-app .\` and \`docker run -p 8080:8080 my-app\`. With version control and Docker plugin, you can perform these actions directly from your IDE.
>
>

> Additionally, you can deploy the local container to a Kubernetes instance on your own computer. I have guided you on how to do this in my YouTube video \[here\]\([https://www.youtube.com/watch?v=mW9H\_rjhdSk&t=4s](https://www.youtube.com/watch?v=mW9H_rjhdSk&t=4s)\).
>
>

## Adding our Continuous Integration Tool

Now comes the interesting part. Up until now, we have been in the local realm. Now, we will build the application continuously and for that, we will move to a distributed environment.

> Again, we could do this locally, but the idea is to get as close to the real world as possible.
>
>

First of all, you need to take care of two things:

- A remote repository where the code base can be pulled to proceed with the build.
- The CI tool.

For the repository, we will choose **Github**.

### Choosing the CI

In the market, there are plenty of CI solutions available. The most popular by far is Jenkins \(although some people find it a bit old-fashioned\).

Besides Jenkins, you also have CI solutions as SaaS/Cloud/Serverless like 

- \[TravisCI\]\(https://www.travis-ci.com/\)
- \[CircleCI\]\(https://circleci.com/\)

and of course, big cloud providers offer their own solutions: 

- \[AWS CodePipeline\]\(https://aws.amazon.com/codepipeline/\) 
- \[Azure Pipelines\]\(https://azure.microsoft.com/es-es/products/devops/pipelines/\) 
- \[GCP Cloud Build\]\(https://cloud.google.com/build\) 
- \[Github Actions\]\(https://github.com/features/actions\) 

to name a few of the most popular ones.

As we are using a public repository on Github, the most convenient option for us is Github Actions because:

1. It's free for public repositories.

2. We have both the repository and CI in the same place, so we don't need additional steps to pull out the code.

### Digging deeper...

Most CI tools define an abstraction named \`JOB\`.

In our case, we want our \`Job\` to build an image of our Java containerized app, but we could also have jobs for running tests, alerting, versioning, etc.

Github Actions \`Jobs\` reside in the same repository as the code.

Below is an example of our \`JOB\` script to automatically build a Docker image from our Java app:

```bash
Name: Build a Docker Image

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
      IMAGE_NAME: "api"
      IMAGE_TAG: ${{ github.sha }}

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Log in to Docker Hub
        uses: docker/login-action@v2
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

Let's break down this file:

We are specifying that the job should be triggered when a Pull Request \(PR\) is made to our main branch:

```bash
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
```

We are defining some variables that we will need later on:

```
env:
      DOCKER_HUB_REPOSITORY: ${{ secrets.DOCKER_HUB_REPOSITORY }}
      IMAGE_NAME: "api"
      IMAGE_TAG: ${{ github.sha }}
```

In the \`steps\` part we are doing 4 things: 

- Set Up Docker. We need it to build our image
- Log in Docker Hub to get the Container as Artifact
- Build and \*\*Push\*\* the Docker Image as we have done locally
- Log out from Docker Hub

## Prerequisites

It's important to note that there are two prerequisites we haven't yet mentioned.

As mentioned earlier, we are no longer in the local realm but in a distributed system. This means that the image must be placed somewhere accessible to different services \(again, thinking about deployment!\).

Now, the question arises... where do we upload the image?

### Introducing Docker.io \(aka Artifact repository\)

There are several options to choose from, but for simplicity and popularity, I've chosen \[Docker Hub\]\(https://hub.docker.com\).

Before triggering the job, it is a \*\*prerequisite\*\* to have a Docker.io account and a Docker repository in place.

> If you want to know how to do this, Google / ChatGPT is your friend.
>
>

I named my Docker repository \`datracka/api\`.

> The Docker repository naming convention is \`\<username\>/\<reponame\>\`.
>
>

### Secrets in Github

You will be working with sensitive data. Therefore, this cannot be publicly written in a GitHub Actions file that everyone can read.

To overcome this limitation, we have Secrets and Variables, which are data you store privately in a key/value repository on GitHub and access by key.

In our example: \`secrets.DOCKER\_HUB\_REPOSITORY\`, \`secrets.DOCKER\_HUB\_USERNAME\`, and \`secrets.DOCKER\_HUB\_ACCESS\_TOKEN\`.

> If you want to know how to create secrets \(it's quite easy\), please refer again to Google / AI.
>
>

### Tagging

With this in place, each time a PR is merged into the main branch, a new container image will be triggered and pushed to Docker Hub.

You might be wondering: an image container usually has a name or tag, so what is the tagging policy here?

Good question! We are using the commit hash as the image \`tag\` for simplicity.

`IMAGE\_TAG: $\{\{ github.sha \}\}`

This means that in your Docker Hub, you will have several images sorted by date with tags like \`api:1b6c21e9d888255ab414acc5cd50459794112312\` and so on

## Summary

That's all. I could delve deeper into many topics such as creating a Docker Hub repo, creating secrets and variables in GitHub, or writing the Jobs, but I prefer to focus on the main goal of this post: understanding CI.

You can find plenty of resources out there explaining how to do all these things, and if I have time, I will create sub-posts on these topics.

Until then, enjoy and have fun with CI.
