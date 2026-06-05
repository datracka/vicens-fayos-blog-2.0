---
id: "1234"
status: published
createdAt: 2026-06-05T00:00:00+00:00
firstPublishedAt: 2026-06-05T00:00:00+00:00
publishedAt: 2026-06-05T00:00:00+00:00
updatedAt: 2026-06-05T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week9.svg
date: 2026-06-05
excerpt: "This week I'm testing tools to keep projects in shape while building with coding agents. The problem: as code multiplies, you lose track of what was built and why. Spec-driven frameworks like OpenSpec fix this by persisting every step, not just the output. The interesting part is wiring it together—Linear, GitHub, and OpenSpec, with CLAUDE.md linking each ticket to its spec. We're still experimenting, and plenty of questions remain."
slug: journal-week-9
title: Journal - Week 9
---
# Journal - Week 9

## Intro

Good weekend morning once more, and welcome to my weekly digest, where I discuss the challenges, learnings, and anecdotes from my daily work as a fractional CTO.

This week I'll be very focused on project management. Although I wouldn't consider myself a pure project manager, I combine my expertise on the technical side with the real-world learnings from managing projects for years.

In this area, over the last few months, I've been experimenting with some AI-related tools to try to reconcile modern development practices (development based on coding agents) with the needs of keeping a project in good shape.

So this post isn't about a new project management framework or the best approaches for resource optimization. It's about my day-to-day testing of new tools.

## Project Management in the AI Era

All of us are using coding agents nowadays. At the time of writing this post, the king of them is Claude Code; I don't know what will come in the future.

So how does it usually start? You're asked to work on a ticket, written in Jira or another project management tool. You open your agentic coding tool and start discussing it. The process can be more or less structured. You can also use parallel agents or just several instances; nevertheless, you end up with a bunch of code that you commit and, after some review, eventually get approved.

The point here is that, in the agentic era, code is a commodity. You easily start several mini projects in parallel, and as the code grows you begin to lose control over what is being generated. From a project management perspective, in a time when writing code means writing specs, you lose track of what has been built and why, and—most importantly—what the current specs of the project are.

Sure, you could ask the agentic tool to understand the project, but the point is that having the changes versioned gives the coding agent a better understanding of the project.

## Spec-Driven Frameworks Come into Play

For me, working based on specs comes very naturally. I've been writing specs for myself and for other developers for a long time, and it's actually how I work best. Unlike some devs who love to jump straight to code and implement, I enjoy working on the scaffolding of what I want to build more than the implementation itself. I have to admit, implementation was always the worst part for me.

> There are other spec-driven frameworks similar to OpenSpec out there, and honestly I haven't tested any of them with the exception of openspec.dev, so I'm missing a bit of context.

The main intent of a spec-driven framework is exactly this: to give the developer some structure to start from in this era of spec-driven coding.

Some developers are already doing this instinctively, asking the coding agent to plan before acting. In some cases that could suffice, but the thing is that when you do only that, you're building without adding any persistence. Whatever process you followed vanishes, and you only keep the output.

With a spec-driven framework (SDF), you keep track of all the steps you took to reach the goal.

## Beyond OpenSpec

OK, so we've covered why OpenSpec could help us build more reliable and well-structured applications—but there's more. What if you bring together your project management tool of choice, GitHub, and an SDF, all at once?

That's what we're already doing.

We start with Linear.app, our project management tool, which is two-way synced with GitHub.

When I open a ticket, a GitHub issue is also opened in the related repo. When an issue is started, when a PR is opened, or when the related ticket is closed, it's moved to the corresponding status (In Progress, In Review, or Done).

OK, this is something we already had before SDF and AI—so where's the link? In our `CLAUDE.md` file, we have instructions for the agent to create the specs using a ticket ID. This way, we can link the ticket to the OpenSpec specification.

## Next Steps

We're still experimenting. There are still a lot of questions to solve.

Should using OpenSpec always be mandatory? Because we've had cases where we forgot to use OpenSpec, some features got implemented anyway, and then the specs went stale.

We'll experiment with adding restrictions to `CLAUDE.md`.

After some time using it, the main thing we've noticed is that it's very flexible. You're not forced to use the tools or commands; it's enough to have OpenSpec installed in the project via `openspec init` to start interacting with it.

Also, what do we do when we have hundreds of features—do all of them have to live in the spec folder? Ideally, they'd live somewhere else, and the best place would be the ticket that initiated the feature. So I'm hoping for an integration between a project manager and OpenSpec along these lines.

## Conclusion

That was all for this week. I think the topic is really interesting, and I'm more than keen to hear how you're using these kinds of tools. As you know, we always have to balance delivering and learning. Learning delays us from delivering, but if we don't learn, we slowly decrease our productivity. Both have to be tackled wisely.

That's all—have a very nice weekend!