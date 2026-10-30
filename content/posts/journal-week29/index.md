---
id: "1234"
status: published
createdAt: 2026-10-30T00:00:00+00:00
firstPublishedAt: 2026-10-30T00:00:00+00:00
publishedAt: 2026-10-30T00:00:00+00:00
updatedAt: 2026-10-30
author_id: "1"
cover_image: images/journal-week29.png
date: 2026-10-30
excerpt: "How I’m letting marketing tune waad’s recommendation engine without touching the codebase — and a hard lesson from real working life: sometimes you can’t gather requirements, and the price isn’t set by your costs, it’s set by what the client can pay. Two stories about building software — and pricing it — when reality refuses to match the textbook."
slug: outsourcing-engine-config-pricing-lesson-economics-taught-me
title: Outsourcing Engine Config, and the Pricing Lesson Economics Taught M
---
## Intro

Hi there, how's it going? Thanks for stopping by this humble post and reading me.

This week I have a couple of topics to discuss with you. First, I'd like to explain the process we've gone through at waad to parametrize how the recommendation engine works. If you want to know more, read [this](https://blog.vicensfayos.com/posts/waad-is-live-building-an-ai-powered-saas/).

I'd also like to talk about a sudden realization I had some time ago that I think is worth sharing.

Finally, a technical note about email deliverability and how to maximize it.

Let's start.

## How to outsource recommendation engine management

A lot is going on inside the recommendation engine. We have several agents working together, plus a deterministic approach — a harness — that helps us deliver value to the client.

To be really effective, this harness has two layers. The first is called the "contract" (thanks Claude for the naming), which is the engineering realm. Here we have engine configuration like which models we use, number of tokens, and so on. But we also have engine configuration that is closer to the marketing realm.

Which objective do we want to serve with our tool? What is the minimum amount we recommend to start a campaign? And the minimum period? Are there special seasons where we know campaigns have to behave in a specific way?

Those are just some of the questions I asked the marketing team in order to start adjusting the engine. But — and here comes the point — the idea was never for me to set the values in stone and deploy the app.

That's not realistic. Those values can be tweaked depending on how the market, the investors, or other factors evolve. I don't want a situation where every time we need to change a value we have to go through a complicated process that could eventually put the project in danger.

So I've centralized all the configuration in a single file that marketing can look at and request changes to on demand — easily, and in an almost secure manner.

OK, maybe you're thinking that a configuration file isn't very flexible — that I've worked around the need to change the codebase (and the risk to product quality that comes with it), but I still need to deploy it. And you're right. For now, I just want to put all the pieces together so marketing is aware of what they can do, even if it isn't 100% flexible for them yet.

Once they start tweaking things here and there, I'll get feedback about their needs, and at that point I'll move everything to a schema + UI setup.

Also, as I discussed in another post a while ago, I worry about the tight coupling between the codebase and the prompts, and about how the prompts are an artifact that should somehow be managed by marketing too. In the end, they define what the agent is and what it can do.

For now, after some testing, I've decided not to do anything about it. In the near future, if I think it's needed, I'll make the prompts configurable too. For now they just live in a folder that's shared with marketing regularly (whenever a related prompt changes).

Configuring them is tricky, because prompts have a part that's engineering and a part that's marketing. There isn't a clear approach to it yet — or at least I haven't found a clear path to follow. What I've been reading suggests splitting the prompts and keeping the marketing side unaware of code injections, then adding some scaffolding to make sure nothing there affects the codebase. It could work, but it doesn't remove the coupling — it just minimizes it.

So for now it's out of scope.

Regardless, I'm happy with how things are moving, and I hope marketing starts using all the tools they have at hand.

### Don't take requirements

If you're an engineer, you know the steps any project is supposed to follow. First you gather the requirements, then you start implementing. Without requirements you can't estimate a scope, and the project can't be monetized.

Is it true? Well, almost.

In a perfect world, yes. I actually believed that not long ago, but then reality hit hard. Sometimes you can't get the requirements — sometimes even the customer doesn't know them.

And this is where price comes in — the money. In the end, sadly, customers mostly care about the price. It doesn't matter how well you explain the importance of building solid software, reliability, scalability, security... they want to lock down what they'll pay you today by asking for a budget, without giving you much information. They want to build a wheel out of a square, somehow. And if you're as rigid as I was, there's only one answer you can give: "without requirements, estimation is not possible." Fine — you just lost the client.

So should you just jump into the void and give a price without any information from their side? Sadly, yes.

A short story: I'm not an engineer — I studied economics. In those studies you learn a lot about how to calculate costs. You calculate the cost of things, then apply a margin, and that gives you the final price, right?

I took Costs I, II, III, and IV... and then, on the very last day, once we'd finished the whole costs sequence, the teacher told us that price is actually set by marketing. Haha.

And that explains exactly what happens now. Pricing from the cost perspective — requirements become hours, and hours × price-per-hour gives the final price — is wrong. You set the price from the marketing perspective — how much they can pay — and then you juggle a bit in case you fell short (yes, that risk exists).

For me this is a masterclass lesson — something you don't learn in any school, not even in a fancy Master's. It's the kind of thing only facing real working life can teach you.

It took me a while to get it. I hope it saves you some years.
















