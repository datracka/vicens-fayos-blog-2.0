---
id: "ambj0bi8QQiUv9vXEOnn4A"
status: "published"
createdAt: "2024-09-18T10:10:40+01:00"
firstPublishedAt: "2024-09-18T10:10:43+01:00"
publishedAt: "2024-09-18T10:12:21+01:00"
updatedAt: "2024-09-18T10:12:20+01:00"
author_id: "156386009"
cover_image: "images/pure_generation_vs_supervised.webp"
date: "2024-09-18"
excerpt: "AI will not replace developers but will enable us to become 10x developers."
slug: "ai-and-the-future-of-developers"
title: "AI And The Future Of Developers"
---

# AI And The Future Of Developers

# Introduction

I could not resist telling you what I think about this topic.

As someone with a strong relationship with IT and development, this topic affects me closely and, like many of us, has been worrying me.

AI, AI agents, reasoning AI, etc. — AI is evolving quickly, and what it achieves seems almost magical.

Nowadays, any developer who does not use AI as part of their daily work will fall behind.

But the real question is: **will AI take our IT jobs in the near future?**

I assert that no, it will not. I come to this conclusion after analyzing my day-to-day work and the existing tools we have available.

That said, it is true that it can replace developers in some cases. But \*\*it all depends on the use case or the problem we want to solve\*\*. Still unclear? Bear with me, and I will show you.

> It all depends on the use case or the problem we want to solve
>
>

To structure my reasoning, I will split AI generation into two categories: "**Pure Generation**" and "**Supervised Generation**" These groups cover two kinds of use cases where AI can be useful.

# Pure Generation

Pure Generation is what we see in influencer videos replacing human effort and creativity. But what do all these examples have in common?

They must satisfy the following conditions:

1. **Output as it is**: The generated content will not need further upgrades or modifications and will serve our goals as it was generated.

2. **The Good Enough Rule**: The generated content is acceptable, even if it’s not exactly what you had in mind.

For example:

For a post I write \(let's say this one\), I need an image. I prompt some text, and I get a generated image. I don’t need to modify it in the future, and it is good enough for my needs.

However, continuing with this example and breaking one of the rules, if the image were for a well-known brand with very specific branding, it is quite unlikely that we would generate the image we really need. Therefore, it wouldn’t be useful.

# Supervised Generation

This category of generation targets use cases where:

- Generated content is suitable for modifications/upgrades
- Complex use cases



We’ve all seen code generation tools that, given a prompt, can:

- Build an app that uploads photos and lists them with a search
- Add authentication/authorization
- Use React and Tailwind
- Add database support

These tools can generate all the necessary files, push them to the repository, and even deploy to Vercel.



But let's split hairs and add other requirements we might have in a typical real-world project:

- The app must separate different domains, such as User and Photos, into micro-services architecture.
- It should run on AWS with EKS.b \(Kubernetes\).
- Authentication must use the company's SSO.
- Follow the company’s CI/CD best practices.
- Requirements are just for the first iteration, following stakeholder needs; the codebase will be modified in subsequent stages by different teams across various countries.

To name a few...

You cannot prompt for all of this at once. You can prompt for parts of it, build blocks, and generate some sections on your own.

# Summary

In the end, real-world use cases are so complex that AI cannot fully meet them.

And I haven’t even mentioned the human error layer! \(I remember working on APIs where the documentation and the actual implementation differed!\)

So, this is the reality of AI for coders: it does not replace us but enables us to be the 10x developers we always wanted to be!
