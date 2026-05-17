---
id: "1234"
status: published
createdAt: 2026-05-17T00:00:00+00:00
firstPublishedAt: 2026-05-17T00:00:00+00:00
publishedAt: 2026-05-17T00:00:00+00:00
updatedAt: 2026-05-17T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week6.png
date: 2026-05-17
excerpt: "As an IT company, or anyone building a product using agentic coding, you want to keep risk as close to 0 as possible. The product should not fail, it should be trustworthy, and at the same time it should be built as fast as possible. The same tradeoff we study in portfolio management appears here as well: lower risk usually means lower profitability, while higher profitability comes with higher risk. And I really think this framework fits the agentic coding discussion surprisingly well."
slug: journal-week-6
title: Journal - Week 6
---
# Journal - Week 6

## Intro

Hi everybody, good Monday morning.

This week I decided to publish the post on Monday, just to test what has a better impact on LinkedIn. I will talk about the main challenge from last week regarding the challenges of architecting a new product, as a continuation of last week’s thoughts.

Also, being part of a fast-paced development team, I want to share my thoughts about agent coding (vibe coding) usage within a team, based on conversations with colleagues about it. You know the topic: how to use it properly, the learnings, the pitfalls, and the different approaches people take.

## Agent Coding

I see this from the perspective of asset management portfolio rules. Besides studying Computer Science, I also studied Economics at university, specializing in finance management and stock markets.

One of the main subjects was asset management — finding the best way to optimize a portfolio of assets (stocks, real estate, bonds) so we can maximize profitability while reducing risk as much as possible.

And this is exactly the approach I would like to transmit when we also approach agentic coding.

In portfolio management, the strategy to follow as a manager was the following: given the accepted level of risk for a portfolio, maximize profitability.

In other words, the fixed variable is risk, and the moving one is profitability.

Of course, you already know the basic rule: lower risk means lower profitability, and higher risk means the opposite.

And I really think this fits the agentic coding problem very well.

As an IT company, or anyone building a product using agentic coding, you want to keep risk as close to 0 as possible. The product should not fail, it should be trustworthy, and at the same time it should be built as fast as possible (profitability).

Here we also have the same distribution of scenarios.

The lowest-risk approach is to use agentic coding to help you find answers that previously you got through a mix of Google and Stack Overflow, and eventually generate some code chunks that the developer can verify before adding them to the production codebase. This is also the one with the lowest profitability, since the speed of code generation is not increasing dramatically.

On the other side, we have what you know as vibe coding by users with poor technical knowledge but a clear idea of what they want to achieve.

Agentic coding produces a huge amount of code (profitability), but it also assumes huge risk as a counterpart (although sometimes the lack of technical knowledge prevents people from seeing it).

If we assign roles to this framework, the ones more interested in profitability would be product-related roles and CEOs, while the ones who always need to minimize risk are the more technical roles (CTOs, tech leads, and developers).

Therefore, if you have followed the reasoning, I think you will clearly understand what my recommendation is from a technical perspective.

Not a single line of code that the team does not understand should be added to the codebase. Because the risk has to stay close to 0, and because I am ultimately responsible if something goes wrong with the product.

Does this finish the discussion? Not at all, unfortunately, because there are a lot of in-between use cases that could allow us (the tech guys) to be more relaxed. The work now is to enumerate those use cases and assign a proper level of accepted risk to each one (always thinking about codebases whose goal is to be deployed to production).

Looking forward to hearing if you have any add-ons to this.

## Architecting a New Product (Part 2)

Last week I wrote about how I approached defining a roadmap that was technically feasible and, at the same time, aligned with business expectations and needs.

We agreed on a bottom line — the red lines that the business required given a delivery date.

During this week I have been bringing the product more and more down to earth, defining how the modules I identified can become reality and understanding the workload they require.

It looks like an arduous task, but the good news for all inexperienced CTOs is that we have tools. But we need to be very creative.

I will try to share some of those ideas here, and I hope they are helpful to you.

### Do It Manually, Then Automate

You already know this dogma: it is 100% true for anything you are doing. First, you have to build all the scaffolding that allows you to do whatever you want manually, so you can have a controlled environment for testing. Then, if you like it, you can automate it. This way, we reduce risk.

You already know that part. What you maybe did not know is that you can also use this approach to reduce scope.

We all love automation — pressing a button and magic happens. But the more magic, the more work.

So anytime you are asked about a complex feature, split the parts that are intrinsically related to it, and separate what is automation from what is not. Because automation does not remove the manual part — the manual process always has to exist first.

You will be amazed at how much extra work an automation layer introduces. Automation assumes a system that has to scale, be observable, and maintain trustworthiness... while still keeping the manual process in place.

Of course, doing this is not free. First, you are passing the workload to others, usually non-technical people who have to do manually what the machine will automate later on. Also, it is a short-term solution, since manual work does not scale. Finally, you may need to create some workarounds for the manual process that will no longer be needed once automation is implemented, but most of the time I have found them acceptable.

### Split, Split, and You Will Find Things You Can Remove

Yes, even if you have a module that is a 100% red line and must be part of the very first MVP version, if you look deeper you can always find — let’s call them “sub-modules” — that can also be removed or delayed to future iterations.

For example, in my case, and without disclosing the product I am building, the “notifications” sub-module was one of them.

Our product needs a way to notify incidents in a centralized and normalized way, but the fact is that, even though it is very important, in the short term it could also be delayed, and we could get all notifications directly from the sources with the help of some handwritten scripts.

### Creativity

In the end, what I am trying to transmit here is that the most important asset is creativity: having a very clear overview of the product you want to build and the ultimate business needs, and building it within all the constraints of a real-world project.

Lack of money, lack of team, or lack of a very clear path — make it happen anyway.

## Conclusion

I think this is more than enough for this week, and these two topics synthesized the biggest learnings and challenges I had.

Of course, this was not everything. I also felt like I was somehow blocking the team, since I had the gatekeeper role for assigning permissions within our AWS cloud platform, and not everything worked the first time. Also, when I defined the stack we will use to build the infrastructure (IaC, CDK, GitHub Actions), I had to run some sessions with the developers to show them the basics of those technologies.

But in the end, I am lucky to have a great team that I can delegate to, and they respond well. So with this asset, I am pretty sure we will overcome all the issues that arise.

I wish you a happy week!


















