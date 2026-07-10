---
id: "1234"
status: published
createdAt: 2026-07-10T00:00:00+00:00
firstPublishedAt: 2026-07-10T00:00:00+00:00
publishedAt: 2026-07-10T00:00:00+00:00
updatedAt: 2026-07-10T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week14.png
date: 2026-07-10
excerpt: This week’s reflection is about flexibility, alignment, and evolution. Business direction can change, especially in startups, and IT must be ready to adapt without losing focus or momentum. As our Marketing AI tool evolves, we are shifting from a model-based recommendation engine toward an agent-based architecture, combining frontier models with our own curated RAG dataset to create a stronger competitive advantage. At the same time, the ERP integration project is back on track, with clear milestones, better rhythm, and positive progress after the first two weeks.
slug: journal-week-14
title: Journal - Week 14
---
# Journal - Week 13
	
## Intro

Good Monday morning, everybody, and welcome back to my weekly digest, where I share the learnings from the journey of building an innovative Marketing AI tool, together with other topics that arise from my daily work.

This week, I’d like to share how IT needs to remain flexible, because changes in direction from the business side are not just a possibility, but a reality that needs to be taken into consideration and prepared for. I also want to discuss how important team alignment is, and how strongly I believe in keeping functional documentation up to date to support it.

There have also been new findings in our journey that slightly change the architecture.

And last but not least, I have good feelings about the ERP integration project.

## Business Does What It Has to Do

As important as building a product is selling it. Actually, selling it is even more important than building it. Creating something without selling it first is a tremendous risk. The best scenario is to sell it before building it, and then build it.

Of course, this is a utopia, because in order to sell something, it has to exist to some degree. Therefore, it becomes an art: a balance between two worlds that move in opposite directions to reach the same goal.

It is like both sides want to reach Australia, but one goes west and the other goes east.

Each domain has its own language and critical paths to follow. I have already discussed the IT side of things extensively, so let’s put the focus in this post on the other side: the selling side.

How do you convince somebody to build something? It is a very hard topic. It involves strategy, narrative, psychology, momentum, and patience.

But even the most intelligent people — and I can assure you I really respect the new senior layer of the business team — can feel disoriented and confused about how to articulate the message so that it reaches its destination. And it becomes even worse when, at the end of the road, there are not only customers eager to buy it, but also investors eager to get a return. Both of them want to hear different things.

Why am I explaining all of this? Because we are now in a phase where we are modifying the foundations on which the product was based, and this has two main implications. I am not very concerned about the first one, but I am more concerned about the second.

The first one is about changing or increasing the scope. We are building the product in a very flexible way, very focused on short-term results, very modular, and with an eye on those foundational modules that we know will not change easily. So I am fine with whatever outcome comes from the new business direction.

The second one does not depend on how I architected the system, but is more human-centered. I work with a mixed team of professionals, but not all of them have previous experience working in startups. Maybe they feel confused or frustrated when leadership sets new priorities. I hope I can guide and support them so they do not feel disoriented. This is intrinsically related to working in a startup.

## Re-architecting the Recommendation Engine

You know I have talked extensively about architecting the system, but every new finding usually means modifying the initial picture I had in mind.

Now we are facing new findings in the recommendation engine. For context, we had architected the system as follows.

We built a model-based recommendation engine. We rely on a frontier model for support, but we build our own recommendation engine from scratch. At the moment, the seed of the recommendation engine is a RAG system powered by a set of curated recommendations. In further steps, campaign results will enrich it.

But in the last few weeks, we have opened another front. Instead of focusing solely on improving the RAG and the dataset, we found that there is a better way to build a model-based recommendation engine.

Actually, it is no longer a model-based recommendation engine, but an agent-based one. This means that what powers the recommendation is an agent: an agent with context and tools, prepared to do the work for us. For that we are using a beta product from Anthropic: Managed Agents

Then, to create a competitive advantage, we will feed this agent with the RAG dataset: recommendations, campaigns, results, and so on. The idea is to beat major players like OpenAI and Anthropic by using their brains, but narrowing and distilling all that power into what our customers are looking for when they come to us.

## Conclusion

In this final section, I just want to highlight the good feeling I am having after taking leadership of the ERP integration project, which, as I discussed last week, was overdue.

Now the project has a new timeline and, at least during these first two weeks, we are on time. I set very ambitious and short-term milestones to track project progress closely, and yes, it is working well. There have been a couple of issues, as always, but nothing major.

That’s all for this week. Have a very good one.

