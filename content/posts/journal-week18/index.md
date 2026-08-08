---
id: "1234"
status: published
createdAt: 2026-08-08T00:00:00+00:00
firstPublishedAt: 2026-08-08T00:00:00+00:00
publishedAt: 2026-08-08T00:00:00+00:00
updatedAt: 2026-08-08
author_id: "1"
cover_image: images/journal-week18.png
date: 2026-08-08
excerpt: Agent engineering is becoming part of every developer’s job. From MCP and agentic frameworks to harnesses and deterministic loops, I share why agents are moving from an AI specialty into everyday software engineering—and an update on our AI recommender.
slug: journal-week-18
title: journal-week-18
---
# Journal — Week 18

## Intro

Good morning, this time from the very nice French coast. Yes, I am on holiday, but I don't want to miss my weekly appointment with you and my professional blog.

This week I want to talk about one _aha moment_ I have had, and also share some updates about Waad. But without further delay, let's start.

## Everybody will be an agent engineer

As you know, as part of the startup I am supporting as CTO, we are building a B2C AI-powered digital campaign SaaS.

Because its foundations are based on AI, I am experiencing all the challenges related to working closely with this thrilling technology.

We have discussed AWS support with Bedrock or SageMaker, how to build RAG systems, and different frameworks and approaches for building agents.

It is this last field that I have become more interested in during the last few weeks. Building an agent basically means moving from text (LLMs) to actions: actually doing things. And this involves implementing code.

It is also deterministic code. All the buzzwords you may have already heard, like "harness" or "agentic loops", refer to making LLMs more deterministic. And you make them more deterministic by, again, implementing code.

So, as you can see, we are (finally!) moving from this blurry Data Science / ML layer, where we were talking about concepts like NLP, tokens, transformers, etc., to a much more familiar field for engineers: **code**.

And here comes the revelation.

If we are building code as engineers, writing code to build agents is nothing fundamentally new. And even more importantly, it is something that every engineer should learn to do.

Yes, every engineer should put an agent in their life.

And there is a parallel with less technical fields. I mean, who can work nowadays without the support of an agent — ChatGPT, Claude, you name it? You need one if you want to remain competitive.

The same applies to engineers. Forget the times when you could develop an application without thinking about agents. Those times are ending. Whatever you build, sooner or later you will probably need an agent somewhere.

To bring this down to earth, let's look at an example.

Imagine you are building a REST API, you know, the classic one that provides functionality to some clients. Previously, you could have built this using a language such as Java, PHP or JS, together with frameworks like Spring, Laravel or NestJS.

Frameworks help you structure the codebase, putting the different pieces you need to build an API together in a way that allows you to scale it in an orderly manner. You could perfectly build an API without a framework, but in practice, you normally use one.

REST APIs are grounded in HTTP and REST principles. You need to understand verbs such as GET and POST, their stateless nature, and conventions around authentication such as OAuth, client/server communication, etc.

But, for example, instead of connecting clients and servers only through REST APIs, you could expose functionality through MCP.

MCP is not exactly the same thing as REST, but it gives us another way to expose capabilities. Instead of only connecting pieces of deterministic code, an LLM or agent can connect to a "tool".

Here, the LLM/agent behaves as the client, while the tool exposes the backend functionality.

OK, so you see where this is going: you could build an MCP layer in your application to provide tools and context to an LLM.

But not only that.

Your application may also use third-party APIs. This is extremely common in microservices architectures, where different services communicate with each other through APIs. You may already be familiar with concepts such as SAGAs, circuit breakers, etc.

And here we are exploring whether some of those interactions could also be exposed through MCP, particularly when an agent needs to interact with those services.

Again, to transform a piece of code into an MCP client or server, you could do it from scratch or use a framework.

Why would you add more complexity to your codebase by adding an agentic framework?

Because it gives you much more power.

An LLM/agent can help you with tasks that previously required a lot of complex functionality to be implemented. They can help with something as simple as extracting a date from a response — although I admit that might not be the best example — or help you build an application that schedules actions in Google Calendar and other tools with relatively little effort.

They can act autonomously.

I have asked my team to start checking the feasibility of replacing or complementing some service-to-service connections with MCP-based ones. I'll keep you updated about what we learn there.

## Building the Agentic Recommender

And yes, besides thinking about putting agents everywhere else, we are still focused on our main use case: a chatbot that recommends a digital advertising campaign mix for your company and can ultimately activate those campaigns automatically.

It is moving at a good speed. We have already built the chat extractor and the recommender. The architecture of the agent tries to be as deterministic as possible.

Actually, I think the work of an agent engineer could be summarized as trying to make agents behave as deterministically as possible.

We have defined our first "harness" and loop iteration, and I think the service will be ready for human testing in one or two weeks.

Then, the next challenge will be figuring out how to automate those tests as much as possible. But those learnings will probably fill another post.

Until then, I wish you a happy August week, hopefully enjoying some holiday days with friends and family!









