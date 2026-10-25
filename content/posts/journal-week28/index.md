---
id: "1234"
status: published
createdAt: 2026-10-23T00:00:00+00:00
firstPublishedAt: 2026-10-23T00:00:00+00:00
publishedAt: 2026-10-23T00:00:00+00:00
updatedAt: 2026-10-23
author_id: "1"
cover_image: images/journal-week28.png
date: 2026-10-23
excerpt: After five months of hard work, Waad is officially live in production! We're entering our Family & Friends phase, testing the platform with real companies. In this post, I break down Waad's architecture, infrastructure, tech stack, AI components, and tooling, along with the decisions and challenges behind building an AI-powered SaaS product.
slug: waad-is-live-building-an-ai-powered-saas
title: Waad Is Live! Five Months of Building an AI-Powered SaaS
---
## Intro

Hi everybody! Another week, another blog post. Thanks for coming back and reading!

Today is a special day. And it's special because I want to announce that **Waad is live and running on production servers!**

Okay, we're not yet open to the world. We're currently in **Family & Friends mode**, where a selected group of companies is thoroughly testing Waad. This is a common approach that helps us improve product quality, fix bugs, and gain observability.

In this post, I'm going to break down what Waad is, what comes next, and the challenges we're experiencing along the way.

I might repeat myself a bit today, as some of these areas have already been discussed in previous posts. Nevertheless, this post should wrap up five months of hard work pretty well.

So, let's start!

## What's Waad?

Waad is a SaaS product that allows small businesses to access the same resources that large enterprises have when it comes to advertising in the digital landscape.

And this is possible because we've entered the AI era, where the power of LLMs and generative AI makes it possible to consolidate and synthesize knowledge that previously required a dedicated team into a single AI-powered application.

Of course, it's easy to say and not so easy to build.

So let's use this post to summarize and celebrate what we've achieved: **Waad is now deployed in production**, and we're entering a new phase called "Family & Friends," where the product will undergo intensive testing.

Let's dive in!

## Building Waad: Pieces of the Puzzle

From a functional perspective, Waad is built around four main components, each of which can be broken down into smaller pieces. For the sake of simplicity, I'm going to stick to the first level and briefly mention the lower layers when needed.

Waad consists of:

- **Product / Shop:** The application that the end customer, typically a company, interacts with.
    
- **Digital Planner & Optimizer:** This is the brain, the AI layer that powers Waad. Internally, it can be divided into a planner that takes a company's brief and produces a proposal for distributing its advertising budget to maximize returns, and an optimizer that runs periodically to fine-tune active campaigns. Both are powered by agents working together in a coordinated way to achieve their goals efficiently.
    
- **Marketing Data Pipeline:** The AI brain needs data to continuously improve its recommendations and optimize running campaigns. This component is therefore critical to the product's long-term success.
    
- **Back-office / Management Tools:** This is the not-so-thrilling part of the product, but it's absolutely essential. It includes all the tools needed to manage generated campaigns, customer accounts, invoices, and, of course, AI-generated outputs, among other things. It's the scaffolding that every digital product needs, the machinery that makes Waad actually work, and work well.
    

If we go deeper, each of these four functional areas is split into several interconnected projects or services.

> We also built marketing websites and landing pages, integrated CRM and marketing tools, and provided the resources that help our business development representatives build awareness and sell Waad. But that's outside the scope of this post.

### Waad Architecture

This brings us to our first technical question: **What's the architecture behind Waad?**

Well, no big surprises here: microservices.

I know this term is controversial. There are both advocates and detractors of this approach to building applications. But you already know my answer: there's no single right answer. It depends.

It depends on the type of project, the scope, the company, the team, their knowledge and skills, and even the timing. Things can change over time.

In a nutshell, I think microservices have three dimensions.

**First, the social dimension.**

Splitting an application into several services makes sense when different teams are working on it. They can work _almost_ independently without overlapping too much or getting in each other's way.

**Second, the corporate dimension.**

Microservices allow a company to be more flexible and align its business units with market needs. If the market requires a new payment approach, for example, the business can focus on the payment service without having to change the entire application.

**Third, the technical and architectural dimension.**

With microservices, parts or modules that previously lived inside a single application or codebase are externalized into components with more focused responsibilities. These components can be developed, deployed, and scaled independently.

Let me give you an example, and a bit of a spoiler about our architecture.

Internally, our Marketing Data Pipeline needs to regularly extract massive amounts of data from advertising campaigns and make that data available to other components, which clean, normalize, and consolidate it.

When I started in the IT world, this would probably have been accomplished with a cron job that periodically exported data, perhaps running on a dedicated server. It would have been used by a single application instance, and introducing redundancy would have required complicated locking and concurrency mechanisms.

Nowadays, we can use a combination of AWS components such as EventBridge, SQS, and SNS to coordinate data extraction and processing across a distributed application running in multiple containers in parallel.

Much of the complexity of managing the underlying infrastructure is handled by these managed services.

Of course, other complexities arise. Distributed systems require more sophisticated approaches to understand what's happening internally (**hello, observability!**), but they also give us the ability to scale.

That said, I haven't split everything into microservices.

Some of our critical business components remain monolithic. Why? Because we're still in a learning and testing phase. We know that many things will change, and we don't want to introduce complicated relationships between distributed systems that would be difficult to modify on demand.

Sometimes a monolith is exactly what you need.

## Waad's Infrastructure

And this brings us to another pillar of Waad: the infrastructure.

I've already disclosed where Waad runs: **AWS**. I've also mentioned that we follow a microservices approach.

Internally, everything runs in containers. For orchestration, we use AWS's own container services.

At the beginning, I was considering going directly with Kubernetes, but I think the ECS/ECR combination is doing a pretty decent job.

Then, of course, we have all the scaffolding that any public-facing AWS application needs: ALBs, CloudFront, Route 53, ACM, SSM, S3, RDS (PostgreSQL), SES for transactional emails, and IAM for access management.

Authentication is delegated to AWS Cognito. Our approach is to focus on core business value and avoid reinventing the wheel.

For LLMs, we rely exclusively on Amazon Bedrock. At the time of writing, we've only tested Anthropic models. They work quite well, and our internal metrics and evaluations indicate that their performance is good enough for our current needs.

There's no reason to invest more time in something that isn't critical right now.

Nevertheless, the LLM we use is configurable.

We also rely on **AWS CDK for Infrastructure as Code (IaC)**.

Almost everything is built with CDK, with the exception of some IAM configurations and a Lightsail server for marketing, which was provisioned manually because it was a one-off request.

I've already talked about this in previous posts, but I love being able to generate infrastructure documentation directly from the codebase. No more stale documentation!

Infrastructure code lives in the same repository as the application code.

You probably already know the philosophy: **You build it, you run it.**

Every developer is responsible for defining and maintaining the infrastructure required by their application.

## The Apps

All this infrastructure supports what actually makes things happen: the codebase.

So I think it's worth spending a few lines explaining the technology stack behind the applications that power Waad.

What I want to highlight here is that **we're not taking unnecessary technological risks**.

Our technology stack is made up of mature, market-proven technologies, selected according to the needs of each application.

Since we have several services, there's no single technology stack.

We have applications running on Java/Spring, others using Python, and others built with Next.js and JavaScript. Our frontends are powered by React and JavaScript.

Pretty mainstream...

We still don't have a Rust project, though. Haha. I guess that's the next milestone! ;)

### Third-Party Dependencies

In some ways, you can think of Waad as an integrator of several external platforms that do part of the work for us.

We're not the ones actually publishing advertising campaigns. For that, we rely on the big players: Google Ads, Meta Ads, LinkedIn Ads, TikTok Ads, and others.

For payments, we use Stripe, although we might move to another provider in the future. We chose Stripe mainly because it was the platform we had the most internal experience with, but its fees are relatively expensive.

As already mentioned, we use AWS Cognito as our identity provider for customer authentication.

We also have a Google Cloud dependency because we use some of the APIs provided by Google, including Google Business Profile, Places, and others.

### How Does It Go Live? CI/CD

To bring all these moving parts into production, we need a proper automated pipeline that builds our artifacts, performs checks, and configures the different environments.

We use **GitHub Actions** for all our CI/CD workflows and jobs, connecting to AWS through OIDC.

We currently have three environments:

- **Development:** Where developers build and test their changes.
    
- **Staging:** Connected to the `main` branch. Every commit to `main` is automatically deployed to staging.
    
- **Production:** We follow the standard approach of using GitHub tags and releases. Only authorized administrators can trigger a production release.
    

This allows us to maintain a controlled release process while keeping staging continuously updated.

## Tooling

Finally, I'd like to finish by talking about the tools we use to make Waad happen.

Not everything begins and ends with [AWS](https://aws.amazon.com/) and [Stripe](https://stripe.com/).

For project management, we use [Linear](https://linear.app/) (love it!).

For source code management, we use [GitHub](https://github.com/) (pretty conservative here).

[Claude](https://claude.ai/) is our AI coding assistant platform (also mainstream).

[Miro](https://miro.com/) is our collaborative whiteboarding tool, and [Google Workspace](https://workspace.google.com/) acts as our company identity provider and collaboration platform.

We also have [Pluralsight](https://www.pluralsight.com/) accounts to keep our skills up to date in this constantly changing world.

And last but not least, we use [Bitwarden](https://bitwarden.com/) as our team password manager.

Nothing particularly exotic, but that's precisely the point. We want reliable tools that help us focus on building the product rather than spending time maintaining the tools themselves.

## Conclusion

I think this post summarizes quite well what we've built over the past five months.

It's been a lot of hard work, learning, decisions, and, of course, changes along the way.

But the important milestone is here: **Waad is live in production!**

Again, we're still in Family & Friends mode. Public self-registration remains closed until we're confident that we can deliver and support all the automations with the level of quality you should expect from us.

And that's our next challenge: moving from building the product to proving that it works reliably for real customers.

Because deploying to production is a major milestone, but it's certainly not the finish line.

Thanks for reading, and see you next week!

















