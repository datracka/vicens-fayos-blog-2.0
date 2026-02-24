---
id: "TQgfWpV7T9ys204cqLd-yQ"
status: "published"
createdAt: "2025-02-06T11:57:40+00:00"
firstPublishedAt: "2025-02-06T11:57:45+00:00"
publishedAt: "2025-02-06T11:57:45+00:00"
updatedAt: "2025-02-06T11:57:40+00:00"
author_id: "156386009"
cover_image: "images/dall-e-2025-02-06-12-56-55-a-humorous-chaotic-scene-in-an-office-where-devops-and-development-teams-are-having-a-friendly-argument-over-a-whiteboard-filled-with-ci_cd-pipeline.webp"
date: "2025-02-06"
excerpt: " In this post, I’ll share key insights to help you avoid the same pitfalls we faced—because trust me, losing hours over misconfigured runtime variables is no fun! "
slug: "next-js-ci-cd-pitfalls-runtime-variable-traps-modern-frontend-architectures"
title: "Next.js CI/CD Pitfalls: Runtime Variable Traps & Modern Frontend Architectures"
---

# Next.js CI/CD Pitfalls: Runtime Variable Traps & Modern Frontend Architectures

# Introduction

As part of a project, I have been helping building the CI/CD pipeline. I had to step in to help because the DevOps and Development teams had started a fight. 🫣

And the application itself was not complex. It was a, at last by now, small project based in NextJS v15, having a Postgres Database for persistence. 

Anyway, building the pipeline was harder than expected due the newest frontend architecture were they can render both in the server and in the client and the nuances itself of NextJS. 

In this post I gonna explain you what you should have in mind to avoid to loose time as we did.

# Next JS Modern Behavior

I won’t go too deep into this, first because it’s not necessary for this post, and second because I prefer not to discuss topics I’m not thoroughly familiar with.

The point here is that NextJS can render on both the server and the frontend. Additionally, it can be built in SSG mode or Dynamic mode \(DSG\)—and oh, there’s also hybrid and other options… things are getting complicated!

> DSG is not a standard term, but for me, it describes an application that, in addition to rendering on the server \(SSR\), is also capable of delivering dynamic content to the client.
>
>

In our case, the last option was the one we wanted. As mentioned, we had a persistence layer \(PostgreSQL\), which, by definition, requires a dynamic application capable of rendering different content based on the state of the database.

# Environment Variables 

Environment variables are how we configure our app for different environments. Simply put, in your local environment, you want \(and you absolutely should, although I’ve seen the opposite happen even in major companies!\) to connect to a local copy of your database.

Similarly, in production, you need a separate set of authentication parameters to connect to your production database.

The same principle applies to other third-party services or environment-specific configurations.

# How This Applies To NextJS 

In an App you can pass environment variables in two ways:

**At Build Time:**  

    Environment variables are embedded during the build process \(usually in a Docker image\). For SSG, this is the only way to pass variables. While it also works for DSG, it is not secure because your secrets could potentially be exposed if someone gains access to your image.

**At Runtime:**  

    Environment variables are provided for each application run. By definition, this method only works for DSG applications. It is secure since sensitive data resides on the server and is never exposed to the client. \(Well, almost—more on this in the quote! 😄\)

> In NextJS, you can explicitly mark an environment variable as public. These variables are sent to the client and are therefore observable by anyone. This behavior is completely independent of whether the environment variables are passed at build time or runtime.
>
>

# NextJS @!\#$!!@

The thing that drove us crazy—and the reason I write this post—is that our NextJS app was not configured as DSG but rather as SSG. The DevOps team wasn’t aware of this and couldn’t understand why the environment variables passed as Runtime weren’t being properly passed to the application.

The reason? In SSG runtime environment variables are ignored. 

> You can find more info here https://nextjs.org/docs/app/building-your-application/rendering
>
>

So, as always in IT, mystery solved, and a new lesson learned—only to be, unfortunately, forgotten sometime in the future! 🤣
