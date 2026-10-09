---
id: "1234"
status: published
createdAt: 2026-10-09T00:00:00+00:00
firstPublishedAt: 2026-10-09T00:00:00+00:0
publishedAt: 2026-10-09T00:00:00+00:00
updatedAt: 2026-10-09
author_id: "1"
cover_image: images/journal-week26.png
date: 2026-10-09
excerpt: Testing LLMs is not like traditional software testing. Their stochastic nature makes consistency and reliability harder to guarantee. This week, I explore how we are testing WAAD's AI recommender using test cases, scoring rules, success rates, and regression baselines to ensure quality as we keep building new functionality.
slug: testing-llms-agents-scoring-regression
title: "Testing LLMs and Agents: Scoring, Consistency, and Regression"
---

## Intro

Hi once again with another weekly post. Honestly, I have to look for a more original greeting, as I feel like I repeat myself a bit every time I introduce one of these weekly posts.

I will ask Claude for some original introductions, similar to the words Claude Code outputs every time it is thinking in the terminal.

Nevertheless, a new week and a new topic. An important topic that I am still learning about: testing LLMs and agents.

Yes, you know that we released one of the products I am collaborating on, "WAAD", in test mode.

Therefore, now it is time to test it and make sure it passes our quality criteria.

It is still a work in progress. I am learning, and maybe next week I will say something that contradicts what I know now. But when learning IT topics, things work like that. Learning a topic takes time, no matter how much AI you have at hand.

## Testing time: Recommender Scoring

So yeah, we are testing the product and, besides the good old testing approaches we have had in the past — you know, unit testing, acceptance testing, integration testing, contract testing, API testing, etc. — we now have a new one: LLM testing, which enriches the existing ones.

Sometimes it sits horizontally alongside them — it could actually be considered a kind of acceptance testing — and sometimes it is a new vertical that has to run in parallel with the others.

Fine, but why is this "LLM testing", or whatever you want to call it, so important?

We need to test the product. The product relies extensively on LLMs to work. LLMs are stochastic. You cannot rely only on deterministic tests — or at least not exclusively; we will come back to that later — because you do not always get the same output from an LLM.

How have we approached this topic?

First, we ran an extensive round of human testing. Some experienced marketers tested the product to check that it works.

But, as you may know: "In IT, checking that something works is the easy part. The problem is being sure that it will keep working."

Therefore, what they did, although important to prove that the product works, is far from enough. We need a way to be reasonably sure that it will always work, or at least most of the time, because again, we are working in a stochastic environment.

So what is the real approach?

Instead of just doing input/output testing to see whether the product returns something correct and meaningful for a given input, we describe the "rules" of the expected output.

I know this sounds quite abstract, so I will use an example based on what we have right now.

We are doing AI-based multi-platform and multi-campaign marketing activation. Given a campaign brief, we output a recommendation for the campaign mix: platforms, channels, etc.

This campaign is also automatically activated, but that is not very important here. What matters is that we are recommending a campaign mix: where to put the money and what exactly to activate. Assets, keywords, topics, publishers, demographics, segmentations — everything that an experienced marketer with years of experience would tell you to create for a campaign, we do for you with the help of AI.

So, to make sure that we are recommending properly, we need to build a "model", an abstraction of what a good recommendation looks like. That is one important part of testing LLMs, but not the only one.

We also need to define test cases so that we have something to evaluate the recommendation against.

For example, we can have a fictional client willing to activate a campaign, but the case can be grounded in real data. That becomes a test case.

For this test case, we can assume that the resulting recommendation should _always_ or _almost always_ contain certain information.

For example, we could assume that when a recommendation includes a Google Ads Search campaign, it should contain at least one keyword including the customer's brand name, or that a Google Display campaign should contain a topic related to a category the customer belongs to.

So we could have hundreds of these checks and run the same test case against the LLM several times. The LLM will sometimes respond well and sometimes poorly, but from those outputs we will capture the variability and be able to say that, out of N runs, each metric achieved a certain success rate.

If we are happy with that success rate, we approve the LLM configuration.

### LLM regression

This approach allows us to build more functionality while being confident that we are not degrading the accuracy, consistency, and reliability of the recommender.

We can define a baseline every time we run the tests and are happy with the results. Once some new functionality is shipped, we rerun the tests. If the baseline does not go down, it means we have not broken anything and we can move forward.

## System vs. Custom

What I have explained so far is a more business-focused testing approach, but from a technical perspective, tests can be divided into two categories: system and custom.

System tests are those tightly coupled to how the system is built. A classic example is tool correctness: are the defined tools called when they should be? The checks here can be mostly deterministic.

Custom tests, or use-case tests, are more related to what the output needs to achieve for the user. They are more subjective, although they can also contain deterministic checks.

For example, you can expect the output to be in the same language as the prompt. If you support a limited set of languages, you can check this easily with code. You do not need an LLM for it.

## Next: LLM as Judge

This is something I am still working on, so I do not yet know exactly how it will work for us.

For now, I understand why it is needed, and it is the next thing I will focus on. But step by step. It makes no sense to open a new door without properly understanding the previous one.











