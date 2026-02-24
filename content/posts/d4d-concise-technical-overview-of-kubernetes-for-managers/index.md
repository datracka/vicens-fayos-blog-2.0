---
id: "RpwyLq3VRAKrIX3mwixV8w"
status: "published"
createdAt: "2025-01-22T09:21:30+00:00"
firstPublishedAt: "2025-01-22T09:21:32+00:00"
publishedAt: "2025-01-22T09:21:32+00:00"
updatedAt: "2025-01-22T09:21:30+00:00"
author_id: "156386009"
category_id: "Z84lDne0Qvi9gJdIH3q5xA"
cover_image: "images/k98s.webp"
date: "2025-01-22"
excerpt: "Kubernetes is an open-source platform designed to automate the deployment, scaling, and management of containerized applications. "
slug: "d4d-concise-technical-overview-of-kubernetes-for-managers"
title: "D4D - Concise Technical Overview of Kubernetes for Managers"
---

# D4D - Concise Technical Overview of Kubernetes for Managers

# Introduction

I have spent several years building CI/CD pipelines for the products and teams I've built and led. While I’ve always been deeply concerned about the importance of having an agile and reliable way to deliver value to customers as efficiently as possible, I often delegated the hands-on work to the DevOps team.



Still, I always felt a bit gutted that I didn’t fully understand the ins and outs of Kubernetes or the advantages it brings.



"It's a container orchestrator," they say. And sure, that's true. But like all good one-liners, it explains everything and nothing at the same time.



I know there are many people out there who feel the same way I did.



In this post, I want to help you understand \_what\_ Kubernetes really is by focusing on its benefits and use cases. This should be especially helpful if you're a CTO or Head of Engineering and need to grasp the essentials.



But before we dive in, let’s start with a brief introduction to \_why\_ Kubernetes matters. If you're already familiar with the usual benefits you hear every time someone mentions Kubernetes, feel free to skip this section.

# Why Kubernetes?



Kubernetes is software you install on your servers, and it magically manages the availability of your applications. Here’s what it does:



- \*\*Keeps your software running:\*\* Ensures your application is always up and available.

- \*\*Simplifies deployments:\*\* Provides a standardized, straightforward way to release new versions of your product securely, using strategies like creating a parallel newer version and gradually redirecting traffic to it.

- \*\*Handles rollbacks:\*\* Makes it easier to roll back in case of issues. \(Though, as they say, "Everything is state, stupid!" Even Kubernetes can't fully solve that.\)



You can associate these three features with "reliability," "trustability," and "availability." I'll leave it to you to match the words to the points.



Kubernetes is also a great companion for a microservices architecture. With microservices, you have isolated applications that must communicate seamlessly. Kubernetes plays a crucial role in making that happen.



So far, nothing new, right? Let’s go a bit deeper.

# Getting to the Backbone of Kubernetes



When you dive into Kubernetes, you start hearing terms like "container," "pod," "replica set," "resource," and "control plane." This is where things often get blurry.



I’ve seen very talented engineers, even from top-tier companies like Red Hat, struggle to explain the foundations of this technology to newcomers. And I don’t blame them—when you’re deeply immersed in a subject, simplifying it for others can be tough.



But trust me, it’s not that complicated.

## Kubernetes Basics, Plain and Simple



First, you have an application. Your application.  

You want to deploy it with all those "-bilities" we mentioned earlier \(reliability, trustability, availability\).  

You choose Kubernetes because you’ve heard about the advantages it offers.

Kubernetes is built around **containers aka pods.**

### What are containers?

Containers are just a standardized way to package an application so DevOps teams don’t need to worry about what’s inside. Think of shipping containers: the crane operator doesn’t care if a container holds a car or 1,000 AirPods. Containers are all the same size and can be managed uniformly.

The same applies to software containers. DevOps engineers don’t care what’s inside; they just grab the container and manage it.

Kubernetes takes the container and wraps it in a **Pod**, which is its way of managing containers and interacting with them.

## Deployments and Deployment Files

Kubernetes handles deployment through a \*\*deployment file\*\* that specifies exactly how your application should be deployed. Typically, you have separate deployment files for each environment: local, staging, production.

This file is not trivial—it’s a fundamental piece of how Kubernetes works. It aligns directly with the current state of your deployment. With this file, you can sleep soundly, knowing all deployment information is centralized and you know where to make changes if needed.

When you update the file, Kubernetes listens and makes the necessary changes to achieve the new desired state—whether that’s increasing capacity, adding dependencies, or deploying a new version.

In the pre-Kubernetes days, deployments involved multiple manual steps that had to be documented somehow. As systems scaled, things became chaotic—no one knew what was applied, changed, or deleted. Total chaos. Kubernetes fixes that.

# Key Takeaways

- Each application or product deployment has a deployment file. The **Source of Truth!**
- Container ≠ Pod, but for simplicity’s sake, think of it as 1 Container = 1 Pod \(even though a Pod can have multiple containers\). It is a common setup.
- Kubernetes automates a lot of heavy lifting for you.

Of course, there’s much more to learn. Kubernetes is complex enough to build an entire career around. There are certifications, career paths, and endless advanced topics. But this post is about simplifying things so anyone with basic tech knowledge can get started.

I hope this helps clarify what Kubernetes is and why it matters.

Thanks for reading!
