---
id: "1234"
status: published
createdAt: 2026-07-24T00:00:00+00:00
firstPublishedAt: 2026-07-24T00:00:00+00:00
publishedAt: 2026-07-24T00:00:00+00:00
updatedAt: 2026-07-24
author_id: "1"
cover_image: images/journal-week16.png
date: 2026-07-24
excerpt: This week I explore the realities of being a hands-on CTO, why we moved our recommendation agent closer to Anthropic’s capabilities, and what building production-grade software with AI taught me about focus, control, and developer quality.
slug: journal-week-16
title: Journal - Week 16
---
# Journal — Week 16

## Intro

Good Monday morning, and thanks for reading my blog once again.

This week, I have some interesting lessons to share from being a hands-on CTO, as well as a couple of reflections about—how could it be otherwise—AI.

So, let’s start.

## Being a Hands-On CTO

As you know, we are a small team. It is not feasible for my only role in the company to be coordinating teams and different company layers. From time to time, I also have to return to the development world and start coding.

One important thing I have learned about managing and coding at the same time is that they are not easy to combine. Maybe some people can do both seamlessly, but I cannot.

I first experienced this around 2010, in my first management position, when I also had to maintain several codebases.

Managing and coding somehow collide.

When coding, you need to stay focused and enter a state of flow. You take a task, concentrate on it and, after a few hours, produce an outcome. Losing that context because of an interruption can seriously damage your productivity.

On the other hand, a manager’s day is full of interruptions that need to be handled. Emails pop up like a popcorn machine. You also have chat messages, alignment meetings, and a myriad of small tasks that you need to push forward.

The only way I have found to combine both responsibilities peacefully is by defining clear time blocks during which I am exclusively a developer. It works for me.

For example, during the morning, I am a manager. After lunch, I block two or three hours to code—or, more accurately, Claude codes and I supervise it.

I learned this the hard way a long time ago.

When you are a manager, you also need to be careful about which coding responsibilities you take on. You do not have as much availability as the developers themselves.

Something unexpected can knock on your door and pull you away from development tasks for days or even weeks, potentially blocking the rest of the team.

## The Development

After sharing these two important lessons, let’s discuss what I worked on last week.

I built an agent: a conversational recommendation agent that can take a user’s input and generate a digital advertising campaign recommendation.

Well, I built its foundations—the backbone. Another member of the team will help me fine-tune the application and turn it into a real production-grade tool.

Why did I do this?

Over the last few weeks, we have come to an important realisation: we cannot fall behind what frontier AI companies such as Anthropic and OpenAI are offering.

At the very least, we need to offer the same level of AI capability as they do. Otherwise, the entire product would make little sense.

During our first iterations, we focused on developing a consistent RAG system. Based on our vertical and functional knowledge, it provides the LLM with enough context to generate a relevant recommendation.

However, we became so focused on improving the RAG system that we forgot about the brain: the agent itself.

During some of our tests, we noticed that regardless of how good the contextual data passed to the LLM was, the resulting channel mix was not of the highest possible quality.

The reason was that the brain was far behind the versions available through companies such as Anthropic or OpenAI.

There was no reason for this to be the case. These companies provide several ways to replicate their agents’ behaviour inside third-party products.

For example:

### Managed Agents by Anthropic

Anthropic offers the possibility of using a sandboxed agent programmatically.

Essentially, it provides an experience similar to what you get through the Claude user interface, but through an API that you can integrate into your own application.

### Anthropic Messages API

Instead of completely outsourcing the agent to Anthropic’s cloud—which is essentially what managed agents do—you can use the agent through an API.

You have access to the full power of Claude’s models and tools, while remaining responsible for building and controlling the agent yourself.

### Final Decision

After careful research, I decided—somewhat unilaterally, I have to admit—to use the Messages API.

Why? There were several reasons.

Using managed agents would simplify the development process dramatically. We would essentially be outsourcing almost everything.

However, we would also lose control.

The chat history and token consumption would be controlled by the managed agent. Of course, we could build a middle layer to store this important information in our own systems, but it would feel somewhat like a workaround. It is not how managed agents are primarily designed to be used.

There are also compliance and legal considerations. For example, where does the customers’ chat history go? Potentially outside the European Union.

The agent’s execution and termination loop would also be almost entirely outside our control. We could configure the system prompts, but not much more.

By using the Messages API, we get the power of Claude’s brain while remaining in control of the agent.

We decide what is sent to Claude, what is not, what is logged, what is persisted, and how the execution flow works.

Yes, we have to build the agent ourselves. However, the MVP use case is not particularly complicated, so the additional control is worth the effort.

## What About the Development Path We Were Following?

Those of you who have read my previous posts may remember that we initially planned to create a recommender service containing both the recommendation logic and the RAG system.

The recommendation itself has now been moved out of this service.

However, the RAG system remains there. Around 80% of the development work—the codebase, database tables, and lessons learned—is related to RAG. The team is still actively iterating on it.

Therefore, none of the work has been thrown away. Only one piece of the puzzle has been moved elsewhere, perhaps temporarily.

It also makes sense from an architectural perspective.

The recommender component exposed an API that expected a very restrictive payload. All the context gathered during the conversation, including the tools used and the previous interactions, would have been lost when calling the REST API endpoint.

In the future, we may decide to move the recommendation brain back into the recommender service, or perhaps into a new dedicated service.

Should that happen, and should we want to preserve all the context gathered throughout the recommendation process, we could connect both agents through protocols such as A2A—Agent-to-Agent.

For now, however, let’s keep things simple.

We have realised that it is easier and more convenient to combine phases one and two of the recommendation process: gathering the information and producing the recommendation.

## Tech Stack

So, what have I actually been doing?

Easy peasy: building an agent.

But how?

I used one of the many agent frameworks currently available. Because this service is written in Java, I chose LangChain4j.

It may not be the fanciest framework, but it provides plenty of useful functionality and abstractions, which are more than sufficient for our current needs.

One of its most useful features is memory persistence, which LangChain4j can manage for us.

What does that mean, and why is it so important?

First, you need to understand one thing clearly: LLMs are black boxes.

You send them a request in natural language, and they return a response. They do not inherently have memory. They forget what you previously sent them.

This is an important realisation.

You may never have thought about it because we are so accustomed to using agents—the web interfaces through which we interact with LLMs—that we assume memory is provided out of the box.

It is not.

LangChain4j takes care of sending the relevant conversation context every time we make a request to the LLM. We do not need to write the entire implementation ourselves, and the context can also be persisted in the database.

All of this is provided out of the box.

### Why Anthropic’s Messages API and Not Claude Through AWS?

We use AWS extensively.

AWS provides several ways to access LLMs through its Bedrock platform, including models from companies such as Anthropic.

Unfortunately, Bedrock was not a good fit for our use case.

Using an LLM is one thing. Using Anthropic’s Messages API and its associated functionality is another. It is a proprietary Anthropic API that is either unavailable or much more limited through AWS.

Therefore, AWS Bedrock was not suitable for us, even though LangChain4j provides reasonably good support for it.

I then learned about Claude Platform on AWS. In theory, it appeared to be a very good fit because it would allow us to use Claude within AWS while retaining Anthropic’s tooling.

However, LangChain4j does not currently support it. For speed reasons, I preferred to stay with Java and LangChain4j.

I did not have enough time to investigate other technology stacks or frameworks, such as TypeScript with Anthropic’s SDK directly. Perhaps that approach would allow us to connect to Claude Platform on AWS—who knows?

For this codebase, I wanted to remain in the Java ecosystem, as it is the language I know best.

Once again, the strategy is to ship something quickly—in September—and then evaluate the next challenges from September onwards.

## Reflections on Using AI for Coding

My first reflection concerns my experience building a production-grade codebase over the last few days.

I have been using AI coding tools for some time, and agentic coding tools since the end of last year, when Claude Code was released.

However, until now, I had mainly used Claude Code to develop proofs of concept or internal support tools that were not intended to run in production environments.

Therefore, I did not spend much time reviewing the generated code. If the output was good enough for the test I wanted to perform, that was sufficient.

This time, however, I reviewed every piece of code produced by Claude and challenged many of its decisions.

I have to say that I am happy with the result, but the process is exhausting.

Historically, a developer’s work had two phases. First, you designed the solution, and then you implemented it.

Most of the intensive thinking happened during the first phase. The implementation phase was generally more mechanical: creating repositories, models, database structures, and so on.

With AI, much of that second, mechanical phase has disappeared.

Instead, you are constantly being asked to make strategic decisions. You need to read Claude Code’s output, understand why it made certain choices, review the code itself, and ensure that you remain in control.

It requires a great deal of mental energy.

Claude Code is incredibly fast. I am not. I am the one slowing down the process, and I know it.

However, I need to remain in control.

Although I could potentially ship four or five features per day by quickly reviewing the output and pressing Enter repeatedly, I have decided to ship only one or two features per day—three at most.

This is a long-distance race. I do not want to burn myself out.

## Developers, AI, and a Final Reflection

My second reflection is not directly related to this project, but I think it is worth sharing.

Before AI, you could usually identify a bad developer after two or three weeks of work.

Now, you may only identify them three or four months later—usually when it is already too late—because they have generated an enormous amount of code, some of which may already be running in production.

Have you had the same thought?

More importantly, what would you do to prevent this from damaging your codebase or product?

That is all for this week.

I look forward to hearing your thoughts. As always, you can find me on LinkedIn.