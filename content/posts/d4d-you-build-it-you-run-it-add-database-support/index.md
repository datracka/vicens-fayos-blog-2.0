---
id: "JWjIQiKlRia7_xnqsAmrEg"
status: "published"
createdAt: "2024-12-28T11:28:19+00:00"
firstPublishedAt: "2024-12-28T11:31:42+00:00"
publishedAt: "2025-01-20T15:39:06+00:00"
updatedAt: "2025-01-20T15:39:03+00:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/database.webp"
date: "2024-12-30"
excerpt: "Integrating database support into your Next.js app with Kubernetes is simpler than you think! "
slug: "d4d-you-build-it-you-run-it-add-database-support"
title: "D4D - You Build it You Run it - Add Database Support"
---

# D4D - You Build it You Run it - Add Database Support

# Introduction

Introduction



Let's say you have a shiny Next.js app with CI/CD in place.



But then the time comes when you need database support to maintain server state. The challenge becomes clear: you also need a Pod in Kubernetes \(K8s\) that contains a database accessible to your app.



No problem! Here's what you need to do:



1. Set up a database deployment in Kubernetes.

	1. Create a Secret to Store Sensitive Database Information

	2. Create the Persistent Volume and Database Deployment

2. Configure your Next.js app with the database connection parameters.

## Setting Up a Database Deployment in Kubernetes

Since setting up the database is a one-time task, we won't rely on sophisticated CI/CD pipelines for this. Instead, this task will be handled by the infrastructure team using Infrastructure as Code \(IaC\) to provision all necessary resources in Kubernetes.

### Create a Secret to Store Sensitive Database Information



First, we need to define some sensitive information:



- \*\*User\*\*: The username for accessing the database.

- \*\*Password\*\*: The password for the database user.

- \*\*Initial Database\*\*: The name of the database we want to create initially \(in the future, you can create more databases if needed—probably! 😊\).



To securely store this information in Kubernetes, we will create a Secret resource. Kubernetes Secrets allow us to manage sensitive data such as credentials in a secure manner.

```bash
kubectl create secret generic postgres-production-secret --from-literal=POSTGRES_USER=<user> --from-literal=POSTGRES_PASSWORD=<password> --from-literal=POSTGRES_DB=<database>
```

### Create the Persistent Volume and Database Deployment

Next, we need to deploy the resources required for the database. This involves two main steps:



1 - Setting up a \*\*Persistent Volume \(PV\)\*\* and \*\*Persistent Volume Claim \(PVC\)\*\* to store the database data.



The Persistent Volume \(PV\) provides the storage resource, while the Persistent Volume Claim \(PVC\) is used by the database to request the storage. Here’s an example configuration:

- **hostPath**: Used for local testing. In production, you might use cloud storage like AWS EBS, Azure Disk, or GCP Persistent Disk.

- **Storage**: Adjust the storage capacity \(\`10Gi\` in this example\) based on your needs

```docker
apiVersion: v1
kind: PersistentVolume
metadata:
  name: postgres-pv
spec:
  capacity:
    storage: 2Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: /mnt/data/postgres
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
```

and Deploying the database itself.

- postgres:17: The image for PostgreSQL version 17. You can replace it with your preferred database image.

- Environment Variables: Securely provide sensitive data using the Secret created earlier.

- Volume Mounts: Ensure the database data is stored persistently.

```docker
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres
        image: postgres:17
        ports:
        - containerPort: 5432
        resources:
          limits:
            memory: "512Mi"
            cpu: "500m"
          requests:
            memory: "256Mi"
            cpu: "250m"
        env:
        - name: POSTGRES_USER
          valueFrom:
            secretKeyRef:
              name: postgres-production-secret
              key: POSTGRES_USER
        - name: POSTGRES_PASSWORD
          valueFrom:
            secretKeyRef:
              name: postgres-production-secret
              key: POSTGRES_PASSWORD
        - name: POSTGRES_DB
          valueFrom:
            secretKeyRef:
              name: postgres-production-secret
              key: POSTGRES_DB
        volumeMounts:
        - mountPath: /var/lib/postgresql/data
          name: postgres-storage
      volumes:
      - name: postgres-storage
        persistentVolumeClaim:
          claimName: postgres-pvc
---
apiVersion: v1
kind: Service
metadata:
  name: postgres
spec:
  type: ClusterIP
  selector:
    app: postgres
  ports:
  - protocol: TCP
    port: 5432
    targetPort: 5432
```

> I recommend you have your own infrastructure deploy where you can organize all those files
>
>

# Repository Configuration

Once the database setup is in place, you need to configure the repository where your application resides.



Since we are using GitHub Actions for CI/CD, this configuration will affect the workflow as follows:



1. Add the database information to GitHub Secrets.

2. Modify the \`Dockerfile\` to accept arguments that will be passed to the application.

3. Update the \`build.yml\` file \(responsible for building the Docker image\) to:

    - Retrieve the secrets from GitHub.

    - Pass them as arguments to the \`Dockerfile\` during the build process.



We are taking the approach of injecting the database configuration during \*\*build time\*\*.

> Note: Another option would be to pass these values during deployment time. However, I encountered issues with this approach, which is why I chose the build-time method.
>
>

## Add Database Info to GitHub Secrets

Store the sensitive database information \(e.g., \`DB\_USER\`, \`DB\_PASSWORD\`, and \`DB\_NAME\`\) as GitHub Secrets. To do this:



1. Navigate to your GitHub repository.

2. Go to \*\*Settings\*\* \> \*\*Secrets and variables\*\* \> \*\*Actions\*\*.

3. Add the following secrets:

    - `DB\_USER`

    - `DB\_PASSWORD`

    - \`DB\_NAME

## Modify the Dockerfile

Update your \`Dockerfile\` to accept build arguments for the database configuration:

```docker
FROM node:18

... 

# Set build arguments
ARG DB_USER
ARG DB_PASSWORD
ARG DB_NAME

# Set environment variables
ENV DATABASE_USER=$DB_USER
ENV DATABASE_PASSWORD=$DB_PASSWORD
ENV DATABASE_NAME=$DB_NAME

...
```

Summary



To integrate database support into your Next.js app's CI/CD workflow using GitHub Actions, you'll securely store sensitive database credentials \(e.g., \`DB\_USER\`, \`DB\_PASSWORD\`, and \`DB\_NAME\`\) in GitHub Secrets.



Then, modify your \`Dockerfile\` to accept these values as build arguments and set them as environment variables. 



Finally, update your GitHub Actions \`build.yml\` workflow to pass the secrets to the \`Dockerfile\` during the build process, ensuring the app is configured with the necessary database connection parameters at build time. 



This approach ensures secure and seamless integration of the database into your deployment pipeline.
