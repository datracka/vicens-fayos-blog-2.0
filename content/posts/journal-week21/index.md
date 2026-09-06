---
id: "1234"
status: published
createdAt: 2026-08-28T00:00:00+00:00
firstPublishedAt: 2026-08-28T00:00:00+00:00
publishedAt: 2026-08-28T00:00:00+00:00
updatedAt: 2026-08-28
author_id: "1"
cover_image: images/journal-week21.png
date: 2026-08-22
excerpt: "This week was mostly about enabling others to move fast: preparing infrastructure, access, APIs, deployment, and a secure Bedrock proxy for our Marketing partner. And after weeks of backend work, we finally reached a milestone: the first conversational UI of our recommendation product is working."
slug: journal-21-onboarding-a-partner-and-time-to-celebrate
title: Journal 21 - Onboarding A  Partner And Time To Celebrate
---

# Journal 21 — Onboarding A  Partner And Time To Celebrate

# Intro

Hi everyone, and welcome back for another week on my blog. Thanks for reading this post.

This week will not be as thrilling as some of the previous ones, where I was constantly writing about my learnings from working with new technologies.

The main task I had this week, besides leading the team and updating stakeholders, was acting as a technical advisor for the development of the Marketing Site.

## Helping Marketing

If you read my last post, you will remember that the week before we selected a partner to help Waad build the Marketing Site.

Marketing needs are different enough from those of the product to justify having their own dedicated business processes, which also influences the decision to have dedicated infrastructure.

The partner agency is working hard on building the application following the business requirements from Marketing. But, you know, this site has to live somewhere, and it also depends on third-party services that we have to provide: APIs they need to consume, email services, CRMs, etc.

All of this has to be prepared in advance so they can start working without delays.

And this was one of my tasks this week — and it still is: preparing everything for them. And I would surprise you if you think it takes just one hour of work. Not at all.

First, I had to set up a dedicated VPS so they could deploy properly. Of course, they also needed a GitHub repository that, for legal reasons, has to live inside our own organization.

Building this can be tricky — or maybe not. The solution I chose, and I am still not sure whether it was the best one, was to give them access to an AWS Lightsail instance. I had heard that these instances were designed to host WordPress sites seamlessly, but after all the work I had to do, I am not so sure anymore.

I wanted them to have enough freedom to create and manage the project, so I gave them SSH access. That means creating users, managing keys, configuring cron jobs, etc.

They also asked to have Continuous Deployment directly from the repository — good for them! — which meant some additional work configuring the GitHub side.

After thinking about it for a while, I decided to build the Lightsail instance manually using the AWS CLI and document everything. I considered adding it to our CDK infrastructure, but in the end, it is just one VPS setup that we should only have to create once.

It also broke the infrastructure model I had originally envisioned, where each project owns its own infrastructure. I cannot allow infrastructure definitions to live inside a project repository that a third-party agency can access.

So this became an exception: a project whose infrastructure lives in our central infrastructure repository. I documented everything carefully so it will also be easy to remove the instance once it is no longer needed.

And then came the APIs.

The final list of APIs they will need is still unclear, but for now I had to create a new GCP account, configure it, and also provide external access to our AWS Bedrock environment.

The most complicated part was configuring access to LLM services.

Initially, I thought about simply providing an easy-peasy Bedrock API key. But after reading quite a few articles about how AI services can be misused, I wanted to add an additional security layer.

Therefore, I decided to build a proxy.

||Bedrock API key|The proxy|
|---|---|---|
|**Spend cap**|None. Bedrock quotas are account-wide, not per key|$175/day, enforced in real time|
|**Per-call cost bound**|None — they control `maxTokens`|Clamped to 1,024; input capped|
|**System prompt**|Entirely controlled by them|Conduct floor appended and not removable|
|**Guardrail**|A request parameter they can omit|Attached server-side on every call|
|**Where it works from**|Anywhere|Only from the Lightsail IP|
|**Revocation**|Requires an IAM operation|Delete or disable one key|
|**Cost attribution**|None|Partner tag|

Again, I hope this was the right solution because it took me considerably more time than expected.

I am still waiting for access to some frontier models, as we currently don't have access to them. Hopefully, AWS Sales can fix that ASAP.

## It Is Time to Celebrate

Yes, not everything has to be about constantly hitting your head against a wall.

That may be 99% of the time, but after all the suffering, eventually the light at the end of the tunnel appears and you finally have something working that you can show to the world.

And this is where we are now.

After a lot of building — first creating the seed of the recommendation model, then building the application, the API, Cognito, security, discussing JWTs, and everything around it — I finally got my hands on this small UI running a fully conversational chat.


![[vicens-fayos-blog-2.0/content/posts/journal-week21/images/backoffice-recommendator.png]]

I know, I know... it is still running locally. We still need to deploy it to the cloud so the business team can actually see it.

That will happen soon.

But for now, I finally have the result of weeks of work in front of me.

## Conclusion

That was another busy week in Hamburg.

There was a lot going on, but I am happy with how things are moving.

Next week, we have to integrate both services, deploy everything together, show it to the business team, and get our first real feedback.

Let's see how it goes!

Have a very nice weekend!




