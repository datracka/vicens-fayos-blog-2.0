---
id: "1234"
status: published
createdAt: 2026-10-02T00:00:00+00:00
firstPublishedAt: 2026-10-02T00:00:00+00:00
publishedAt: 2026-10-02T00:00:00+00:00
updatedAt: 2026-10-02
author_id: "1"
cover_image: images/journal-week25.png
date: 2026-10-02
excerpt: "Engineers and salespeople pull in opposite directions: build first, or sell first? This week I joined discovery calls with our CEO and learned why the balance matters. Plus some technical notes on client/server in LLMs and agents — why the agent is always a client of the model, and where MCP, stdio, and SSE fit in."
slug: sell-first-or-build-first-llm-agents-client-server
title: Sell First or Build First? Plus the Client/Server Model Behind LLM Agents
---

## Intro

Hi everybody, here I am, back as promised after some days off, with a lot of stories and learnings to share with you.

This time I want to talk about something different: how necessary the sales layer is in a company. Over the years I have learned to respect and love selling. It was not a straightforward process.

Besides this, I have — as always — some technical notes I'd love to share with you.

## To sell or not to sell, that is the question

You know what engineers usually think about people who sell. They always get engineers into trouble by selling things before even asking whether it's possible to build them. Then they come with the request and engineers have to scramble to make it happen — most of the time on very flimsy ground, because of the time pressure.

But the thing is, without selling there is no company. From an engineering point of view, the best scenario would be to build it and THEN sell it. From a sales perspective, the best would be to sell it first and then build it — because it's a huge risk to put time into something that might eventually never be sold.

Of course, those are both extremes. You can't just sell it and build it later; that wouldn't work. And you can't just build it and then see if it's sellable; that's too much risk. The balance is in the middle, and this is where empathy comes in — understanding the other's needs and putting yourself in their shoes, something that comes with experience.

As part of my role at waad, I had the opportunity this week to join the business development department and the CEO on some discovery calls. I really enjoyed seeing how they put the product we have built into perspective so that leads and potential customers can understand the benefits, and how they handle objections. And I was there bringing solidity to our proposal, showing them that we are not selling smoke but a real product.

## Understanding Client / Server in LLMs / Agents

This was an aha moment for me when I was learning to use agents properly and programmatically. Agents live on the server but can also do things locally, so it's important to know what they can do in each environment.

> By the way, I don't like referring to Claude or ChatGPT as LLMs anymore. Yes, LLMs are the brain powering the whole conversational input/output loop, but the thing we interact with is the agent. Agents are the ones that actually do things.

I won't go technically deep on this. You can just ask Claude about it and you'll get a comprehensive explanation — but you have to be aware that you _can_ ask this. And that's the point of this section.

But here are the things you should take with you.

**1 —** The agent can be a server-side app plus a client web app, BUT it is always a client from the LLM's perspective.

So, important takeaways:

The model does not have memory, and you have to build all of that yourself. In fact, that's a big part of what agents do.

The model does not do anything. Once you get feedback from the model, if you want to DO things, that's on your app.

And you don't want things to be done without control, so this is where the harness and all the determinism you need come in.

> Important concept here: adding determinism is your job as a developer.

**2 —** How this affects us when we talk about tool use. Tools can be used both server-side and client-side.

By "client side," remember that in the context of agents — regardless of whether they are a backend app running server-side — they are clients of the LLM.

Therefore, all the tools YOU call are client-side. BUT they can be called either from your server or from the machine the agent is running on (localhost).

If you call them from your machine, you'll usually see STDIO in place; if you call them from your server, you'll normally use SSE.

Some people still confuse this. I was reading an article about two ways of using tools through MCP (stdio and SSE). These two ways of talking to external systems are already a bit old, and they were built before all this LLM stuff even existed.

stdio is the standard way to communicate locally between services — very flexible and powerful, and it fits LLM use well. SSE, on the other hand, is a web API you can use over HTTP, which makes it very REST-friendly. It's a very good fit for the use case of sending messages (chat), so it's a good friend of LLMs.

The point here is that we have ways to talk (yes, in this case it's not a metaphor — we really are talking) to external / remote / distributed systems, and relying on existing, battle-tested technologies is the way to go.

BUT LLMs sometimes have infrastructure wrapped around them, and they are not just dumb — they also have access to some tools. So the LLM alone, because it is not a pure LLM, can decide to call tools by itself.

And this is where MCP comes in — basically a collection of tools you can use, remotely, from your client agent on its server-side layer.

Complicated, huh? Yeah, take your time. But you need this mental model if you want to say out loud that you are an AI engineer.










