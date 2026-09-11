---
id: "1234"
status: published
createdAt: 2026-09-11T00:00:00+00:00
firstPublishedAt: 2026-09-11T00:00:00+00:00
publishedAt: 2026-09-11T00:00:00+00:00
updatedAt: 2026-09-06
author_id: "1"
cover_image: images/journal-week23.png
date: 2026-09-06
excerpt: "This week, integration surprises exposed a gap between our AI recommendations and real ad activation. I also explore the coupling between semantic prompts and deterministic code—and the testing challenges it creates. Finally, after 25 years across development, management and startups, I ask myself: what do I do?"
slug: journal-23-integration-surprises-ai-semantics-and-the-question-of-who-i-am
title: Journal 23 — Integration Surprises, AI Semantics, and the Question of Who I Am
---

# Journal 23 — Integration Surprises, AI Semantics, and the Question of Who I Am

# Intro

Hi, and welcome back to my journal for another week. I hope you had a great week and took some time for yourself and your family. Work is very important, but it is not everything.

It is also good to take some time to make room for other ideas—the ones we tend to leave aside during our daily work when we are focused on delivering and being productive.

So, what has been on my plate this week? Several topics.

From my daily work, nothing new: just the integration issues you can expect when putting all the pieces of the puzzle together.

I also want to discuss an AI architectural problem that I have noticed over the last few weeks and for which I would love to find a long-term solution.

Lastly, I want to share a thought about myself and how I am handling my career.

Let’s start without further delay.

## “I didn’t know.” “Nobody told me…”

Yes, you know them. Those two sentences—and many others like them—are among the most commonly used when teams integrate systems that were not previously connected.

You have several teams or people building things in isolation, assuming that the other systems will work as they expect—but they don’t.

Of course, we already know the solution: communication and early integration, so that problems can be identified beforehand and as soon as possible.

I tried hard to make that happen, and I think it worked quite well. Nevertheless, no matter how much effort you put into something, nothing is perfect, and misunderstandings happen.

Last week, the lead developer responsible for the service that publishes ad campaigns and I were discussing the API we wanted to use and how to translate the recommendation provided by the AI into ad activation.

> We are building an AI-powered SaaS application that autonomously activates ads across multiple platforms. The recommendation is the AI’s suggestion about which platforms and channels to activate.

I told him that something was unclear to me, so I started digging into the documentation and asking Claude about it. The next day, when we met again, I shared my findings with him—and then the party started.

We were both surprised to discover that the original payload and API signature we had agreed on were far from what we actually needed to activate campaigns.

Yes, we had the percentage allocated to each platform and channel, but he needed all the related information about _how_ to activate the campaign. This was also part of the recommendation.

He wondered aloud how it was possible that we had reached this point in the project without anybody noticing it.

Perhaps, in the heat of battle, it happened because this was not the main area of responsibility for either of us. Perhaps nobody had taken the time to investigate the advertising platforms and understand what they actually required.

Whatever the reason, this was where we were. Everybody was busy with their own tasks, and we needed a solution. The only person who could jump on it without leaving other top-priority work unattended was me.

So, being the hands-on fractional CTO that I am, I jumped in.

That is what I have been working on for approximately five days. Around 20 merged PRs later, the fix is now in place.

The recommendation payload is now something that can _actually_ be used to activate a campaign.

## The AI semantics issue

Here is another topic that emerged from working with AI-based applications.

You have prompts: prompts for each agent, system prompts, and parameterized system prompts.

You also have LLMs: brains that act and respond probabilistically based on the instructions you give them.

This semantic layer is completely separate from the deterministic codebase, but it also has a significant influence on how an application behaves.

At the same time, we want to add limits—a harness, to use one of the most hyped words of recent months—to constrain the model.

One of these constraints is what we call structured output: the model must return its response in a specific format.

However, this means coupling semantic prose—the prompt—with structured code. If the prompt changes and you do not change the code, the output may break. Both need to evolve hand in hand.

So, how can we handle this?

You cannot simply add static analyzers as you would with a traditional codebase. There are some possible solutions, although none of them is complete.

I have read about treating prompts as versioned artifacts. That is fine, but it does not solve the underlying problem: a new prompt version can still break the output without you being aware of it.

Another option is to add more testing at the evaluation layer. This can solve the problem, but it also adds more complexity. You need to test the outputs specifically against datasets containing expected results.

A third, still largely unexplored approach would be to establish good practices for writing system prompts. We could even structure them in a way that makes them easier to analyze using tools—both deterministic and AI-based ones, of course.

I have been looking for information about this topic, but I have not found much. If anyone knows of a useful resource I could learn from, please let me know. You can find me on LinkedIn.

## The T—and who I am

I have many years of experience across several fields. I have always been interested in understanding all the skills involved in building a digital product.

Of course, you cannot know everything. Nowadays, building something requires a myriad of different skill sets and professionals: POs, PMs, EMs, software developers, database specialists, ETL developers, DevOps engineers, SREs, AI reliability engineers, and RAG experts, to name just a few.

Then there are all the technologies involved, but I will not list them here because I would never finish.

I started my career as a developer in 2001, and I loved it. Later, I moved into management—in a role similar to Technical Director, but also involving project management. Then I became a startup founder, which gave me the opportunity to work with other areas, such as infrastructure.

In the meantime, I also did a great deal of freelance work as a software engineer. I have managed teams and projects and designed architectures across several technology stacks and cloud environments.

That is a lot of different experience.

But after all this, if somebody wanted to hire me, what exactly could I offer?

Honestly, I don’t know.

I always say that I love building products and pushing them forward. I consider myself very organized, and I care about the small details that can make a project succeed.

But undoubtedly, I also have shortcomings.

I have never been able to stop learning and moving forward. I have embraced change—perhaps too much?

I have had a 25-year career, and if you asked me what I do, I would still struggle to give you a clear answer. 









