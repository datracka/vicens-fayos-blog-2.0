---
id: "1234"
status: "published"
createdAt: "2026-04-08T00:00:00+00:00"
firstPublishedAt: "2026-04-08T00:00:00+00:00"
publishedAt: "2026-04-08T00:00:00+00:00"
updatedAt: "2026-04-08T00:00:00+00:00"
author_id: "1"
cover_image: "images/journal-week1.png"
date: "2026-04-09"
excerpt: "A reflection on the first week of building an AI-driven retail product: from shaping a lean team and defining the first `showable` version, to letting go of control and embracing uncertainty in early-stage development"
slug: "journal-week-1"
title: "Journal - Week 1"
---

# Journal - Week 1

## Introduction

I have just started a new project, helping a group of entrepreneurs to build the next retail ad automation application, heavily based on AI, and the very first weeks have been a ton of challenges.

From building the team to architecting the system and supporting Business Development in selling across many fields that, although I had experience in, always bring important learnings.

So I took the decision to write a weekly journal to reflect and not forget all the things that I have been experiencing.

This journal will not only be related to this client, but also to any other challenge I experience while helping my clients that I find worthy to publish.

Let's start.

## Challenges / Learnings Week 1

- How to implement lean but meaningful processes in a new team  
- Building the Happy Path for the very first "showable" version of the product  
- Code as disposable  
- My own fear: blocking the team  
- Raising of the Agentic UX/UI  

---

## How to implement lean but meaningful processes in a new team

I have to accept I will not be a perfect Product Owner, nor an architect. I will keep within the basic limits.

Be very efficient in communication, and don’t produce useless or redundant documentation.

The only important documentation at this stage, IMHO, to avoid disappointing the business or disorienting development and making them work in vain, are alignment documents. In my experience, they are very important if the product expectations are written in black and white.

Conversations and decisions get lost over time, therefore.

Therefore, we are working on building functional documentation that, at the end, will have to be approved by Product. I know it will not be perfect, and through iterations it will change a lot, but I will push the team to keep this document as up to date as possible.

Also, I implemented 2-week sprints, but very loose ones, just to stay focused.

We meet at the start of the week, we commit to a set of tasks with a clear and verifiable way to check them, we write them down in an Excel, and at the end of the sprint we check if we accomplished them or not. We also do a retrospective.

I don’t have a PM / ticketing tool yet; it is not needed at this stage.

Of course, we do our daily — it is very important to stay in contact because we are working remotely.

---

## Building the Happy Path for the very first "showable" version of the product

When we started scratching the surface of the idea the visionaries had, we quickly saw there is a vast amount of functionality and many critical parts. And I am even leaving aside infrastructure, CI/CD, and other tasks not strictly related to the product.

Given the size of the team, and even with coding agents, it is very important to constrain what we want to deliver the very first time the product is showable.

It involves defining a Happy Path — some assumptions the user will take that will save hours of work and problems.

As a matter of example: our customers can have their own web page or not, a Facebook page or not. We will cover all the cases in the final version, but for the first one we assume a client does not have a web page but has a Facebook page.

> This decision is agreed with Business

---

## Code as disposable

This topic is not new, and maybe you have reached the same point, but the thing is that nowadays, as code is a commodity, building a parallel UI to the one that will finally be shown to the user is not a waste of time — it is just a matter of spinning off another agent.

This is just an example, but I think you get the point. Always ask yourself if you need any coding support along the way.

---

## My own fear: blocking the team

I have always been afraid that the team is not optimized to the maximum, that it is not performing as well as it should, and that there are idle hours where people don’t know what to do.

The solution to this has usually been to ensure that everyone carries out some prior work, typically functional documentation, so that the person or the team clearly knows what to do and stays aligned.

Unfortunately, on this occasion the tasks to be carried out are so vast that it is not possible. I myself need to understand many high-level aspects before I can tell the team what they should do.

That said, I can see that they are unfocused, without a clear output of what they are supposed to deliver. Happily, I also found a solution: just give them enough space to suggest and to find their own way to solve the problems. I am just acting as guardrails when I see they are going too far.

For example, one member of the team, very smart, has the task of building a RAG PoC for our AI-powered recommendation system. It is a fairly complex task for this project, with a lot of new concepts to learn.

The initial instructions I gave him were ignored, and he followed his own path. Part of this path has been to configure Claude Chat with a system prompt to behave as expected when communicating with the user.

After discussing and understanding why he focused on this area and not on learning about the data we have in place, how to build the chunks, and how to ingest them, I let him move forward.

But I also told him to do everything needed for the functionality of the RAG and to forget any UX temptation that can come from working with LLMs.

At the end, everything falls into place by itself.

---

## Raising of the Agentic UX/UI

I left this point for the end. For me, it has been the most interesting finding in this very first iteration.

Adding LLMs to build apps changes the game on the infrastructure side of the application, but also on the UI/UX side.

We have to avoid, as much as possible, complicated forms that were previously unavoidable because use cases were very complex.

The key idea: everything can be integrated into the AI chat.

I am not saying everything should be integrated — we have users who are very well trained in many UX patterns, and they know where to look for a login button and how to open a menu — but it adds a new and very interesting layer that can keep UX/UI designers entertained for a long time.

I am also evaluating whether it would be possible to add all the functionality directly into an existing agentic chat like ChatGPT or Claude.

---

## Final thoughts

This is all for this iteration. I hope it helped you somehow. Stay tuned for more regular updates.

> Note: NOT AI-generated at all. I only passed it, after writing, through Claude to correct grammar errors as I am not a native English speaker. BUT the main ideas and ways of expressing them remain untouched.