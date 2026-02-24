---
id: "WQu9uMh9TGq-2po0MXH2Pg"
status: "published"
createdAt: "2024-07-04T11:19:11+01:00"
firstPublishedAt: "2024-07-04T11:19:35+01:00"
publishedAt: "2024-07-04T11:33:40+01:00"
updatedAt: "2024-07-04T11:31:09+01:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/devops_software.webp"
date: "2024-07-04"
excerpt: "Kubernetes is not only a container orchestrator. It also serves as an infrastructure abstraction, and when embraced, it clearly defines responsibilities,"
slug: "hi-devops-software-developer"
title: "Hi DevOps Software Developer !"
---

# Hi DevOps Software Developer !

# Introduction



From working with my last client, I was involved in many daily DevOps tasks that I would like to share with you.

What I liked most was how software developers had to engage in daily DevOps duties and how elegantly these duties were divided.

# The Set Up



The client was relying heavily in AWS for the Cloud and also K8S for distributing the apps The client was heavily reliant on the Cloud for the cloud and also on Kubernetes \(K8S\) for distributing the apps smoothly among environments, from the Development Computer to Production.

So, given this setup, how does it affect our Software Developer day-to-day?

Kubernetes is not only a container orchestrator; it is also an infrastructure abstraction because:

- Clusters and Nodes were what were previously virtual machines and clusters of them.

- Pods and Containers are abstractions of the application and how it is split into modules to make it more resilient \(for example, you can think of splitting an MVC Web App into FE, BE, and DB pods\).

> Note: I assume you have some familiarity with Kubernetes concepts!
>
>

Therefore, developers will be busy managing the containers and pods while the DevOps engineer will take care of what is exclusively infrastructure.

Essentially, the DevOps will prepare the entire infrastructure so the developer can deploy his pods as required.

# Going Deeper as A Developer - Deployment



Following this explanation and connecting these two concepts, we find:

Containers and Pods are related to the \`Dockerfile\` and \`k8s deployment file deployment.yml\`.

Now we uncover the concept of Deployment.

But... Isn't it a DevOps duty to deploy the application the Software Developer is working with?

YES and NO. The DevOps ensures that everything is in place to deploy the application successfully. The cloud is in place, as well as the CI/CD automations, etc.

But HOW to deploy the application is also a responsibility of the SW Engineer.

Indeed, the deployment descriptor is a file that has to be supervised by DevOps teams, but it is also clear it is something intrinsically related to the Application, because the application deploys on its own in its own Node.

Therefore, the Developer also has a say in it. For example, which constraints to apply to the deployment or how many replicas to have \(remember, we are busy with Kubernetes!\).

So, given a simplified workflow, these would be the responsibilities of a SW Engineer \(the yellow ones\). 



I have become technology agnostic by now, relying only on Docker & K8S for infrastructure abstraction.

However, it is worth noting that the cloud could easily be AWS EKS, for example. The artifact repository could be Docker Hub, to name the most popular one, and the CI/CD could be GitHub Actions.

> I mentioned these technologies because I am preparing some other posts and videos to demystify DevOps for a Software Engineer. So, stay tuned!
>
>

# Wrapping up

DevOps is not just about some people busy with the cloud and IaC terms; it also embodies a broader philosophy of work and best practices to deliver highly scalable and available applications with reduced time to market.

For this, Software Engineers must align with DevOps concepts and concerns and work collaboratively.
