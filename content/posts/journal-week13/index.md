---
id: "1234"
status: published
createdAt: 2026-07-05T00:00:00+00:00
firstPublishedAt: 2026-07-05T00:00:00+00:00
publishedAt: 2026-07-05T00:00:00+00:00
updatedAt: 2026-07-05T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week13.png
date: 2026-07-05
excerpt: This week was all about difficult trade-offs. We reduced the MVP scope to meet an ambitious September deadline while keeping the architecture ready for future growth. We also settled on a modular monolith supported by external services, reinforced our cross-functional team approach, and I committed to turning around a struggling project. Sometimes progress isn't about flashy milestones—it's about making the right decisions that quietly set the foundation for long-term success.
slug: journal-week-13
title: Journal - Week 13
---
# Journal - Week 13
	
## Intro

Hi there, and welcome once again to my journal, where I share everything that has happened and everything I've learned throughout my career.

This week, although a lot happened as always, I don't really have the feeling that there was one major topic I could package into a post.

There were plenty of day-to-day business discussions, another iteration of the MVP architecture (how many have I already written about?), a trip to Madrid to present to the board how we are positioning the marketing tool I'm helping to build, and many more discoveries about how to properly build agentic systems, among other things.

I'll try to summarize all of them, so let's get started.

## The Umpteenth Architecture Iteration

I think I'm probably boring you with all the architectural decisions we're making. I could actually build a timeline covering every decision from the very beginning, all the conversations with the development team and the business, the initial findings, and where we are today.

Where are we now? Basically, we have dramatically reduced the scope to meet the very ambitious deadline agreed with the business: an MVP by September.

This is a commitment I would never have made three years ago, before AI. It would have been suicidal. For the kind of application we're building, delivering in less than six months simply wouldn't have been realistic.

But we live in the AI era, where teams are supposedly 10x to 100x more productive, right? So let's see. It's a bold bet, and I don't have any previous experience to compare it with.

Nevertheless, while we've reduced the scope to increase our chances of success, we're also trying to seed the project in a way that doesn't compromise us too much in the future.

The final architectural decision, at least for now, is to blend several planned microservices into a single modular monolith. It makes a lot of sense at this stage. Microservices wouldn't really help us split the SDLC with such a small team, and we also want to minimize the communication layer between services.

At the same time, it's perfectly possible to build a well-structured system within a monolith by splitting it into modules, defining clear contracts, and designing a solid database model.

## But We Still Use Services

That doesn't mean we aren't relying on services. Even though we're consolidating our core domain into a single application, we still support it with several external services.

Last week we defined the scope and functionality of both the communication platform and the identity provider.

Since we're heavily invested in AWS, we'll most likely use SES together with an SES wrapper (we're still deciding which one) as our email platform. For this iteration, email will be our primary communication channel. Future iterations will also include SMS and, eventually, push notifications.

As our identity provider, we'll stick with Cognito. It's a natural fit and only requires a few adjustments to our current architecture.

## How We Structure the Team

This is something I'd still like to explain better.

The reality is that we're a small team, so we can't afford to work in isolated silos where everyone owns only one specific area. That simply wouldn't work.

Instead, we need to become a cross-functional, domain-oriented team where everyone can contribute across different areas.

I know this adds complexity to communication, and some people don't feel comfortable working outside their own expertise. They often feel less productive and slower than if they handled everything themselves.

But I believe that's just a matter of structure and workflow. With the right processes, tasks can be shared across the team without creating additional overhead.

## Making a Project Successful

In previous posts, you may remember I mentioned a project that was far behind its original deadline.

A lot has happened over the past few weeks. People have left, priorities have changed, and circumstances have evolved. But I couldn't leave the project in that state. For me, it would have felt like a personal failure if we didn't achieve the agreed outcome.

So I spoke with the CEO and personally committed to making it happen, without any additional compensation. That means building a new team, redefining the strategy together with the third-party consulting company responsible for the implementation, and relaunching the project.

I know exactly where I want to take it, and we'll get there.

I'll keep you posted.

## Conclusion

Looking back, I actually accomplished quite a lot last week, even though I lost almost an entire day because of the last-minute trip to Madrid.

The next few weeks will be crucial.

We need to stay focused, keep our goal crystal clear, and work as efficiently as possible to achieve it.








