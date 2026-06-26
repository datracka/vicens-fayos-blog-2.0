---
id: "1234"
status: published
createdAt: 2026-06-26T00:00:00+00:00
firstPublishedAt: 2026-06-26T00:00:00+00:00
publishedAt: 2026-06-26T00:00:00+00:00
updatedAt: 2026-06-26T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week12.png
date: 2026-06-26
excerpt: "This week I reflect on two lessons: why I chose a modular monolith over microservices for an early-stage product after listening to my team, and why perseverance matters when projects don't go as planned. Architecture and leadership often have one thing in common: knowing when to change your mind."
slug: journal-week-12
title: Journal - Week 12
---
# Journal - Week 12
	
## Intro

Hello everybody, and thanks for reading my blog once again.

Today's post will be very architecture-focused, but it is also about leadership (or at least what I believe leadership is).

Besides that, another topic from this week is how important it is to stick to the plan and persevere.

And that's enough for the introduction. Let's jump straight into the topics.

## From Services to Monolith

Ok, this topic is full of videos, books, posts, and opinions. Some people praise Service-based architectures, while others complain about the extra complexity they introduce and the costs they bring, especially for startups.

I have worked with both architectures, and I don't marry either of them. Nevertheless, for this project I was trying to find a good balance between both worlds. Splitting the whole project into microservices—Campaign Service, Payment Service, Customer Service, and so on—would have made the project non-viable. Building everything into a single application (or two, you know, the classic frontend/backend application), although possible, would have meant mixing several domains in one place.

For me, the key question is always: starting from the baseline of "everything is a monolith," which parts can I extract that make the system more reliable, flexible, and scalable without compromising the scope, and therefore without adding unnecessary workload?

From that reasoning, some services were easy to extract. Everything related to the AI campaign recommender/optimizer, authentication, and payments naturally fit as independent services.

Initially, I was also thinking about splitting the service responsible for activating and aggregating campaigns. Theoretically, activating campaigns across multiple advertising platforms makes perfect sense as its own service. It could even become a product by itself.

But that will not be the case, at least for now.

After discussing the topic with the developers, I initially remained firm in my decision. However, I genuinely wanted to understand the point of view behind the objections they were raising. Most of them made a lot of sense. I kept asking questions and we had a healthy debate. I wanted to understand why the lead developer was so strongly against my design.

Then I stopped talking and started listening.

He talked for quite a while, not always in a structured way, but he described many trade-offs that would appear if we followed my proposal. Eventually, I realized that his point of view was more accurate than mine, especially when he explained how error-prone (see the note below) the system would become if we followed my original architecture.

> To keep a multi-service architecture affordable at this stage, I was intentionally shifting part of the operational workload to humans through manual processes. It was one of my "tricks" to keep the scope realistic. You can read more about that in one of my previous posts.

Error-prone. Human complexity.

That was the point of no return.

I thought, _this is simply not sellable_. Although technically we could implement strategies to avoid dramatically increasing the scope while keeping the Campaign Manager as a separate service, the friction for administrators and business users would simply be too high. They would constantly struggle with the tool, and that was not acceptable.

Therefore, I accepted that, for now, the Campaign Service will remain part of the monolith.

That does not mean we will build a tightly coupled application. This component will still be developed as a Spring application using multiple modules, interfaces, and contracts to keep it properly decoupled. The database will also be organized into multiple schemas to provide clear namespace separation.

The idea is to split the monolith into independent services as soon as it becomes worthwhile.

But not yet.

The key lesson for me was that I listened to the lead developer. At first, I was reluctant, but his objections were solid.

He was right.

I wasn't.

## Perseverance

Sometimes you scope a project, create your estimates, and later discover that reality doesn't match the original plan. The project takes much longer than expected, and eventually the stakeholders decide to cancel it.

That is what recently happened to me.

Well, the project is not completely cancelled, but most of the people working on it have been reassigned to other priorities. Without those resources, it simply won't be possible to finish it.

I always feel bad when this happens.

"Make things happen" has always been my motto.

What makes this situation even more frustrating is that I had several ideas that could have dramatically accelerated the project and allowed us to finish it in much less time. Unfortunately, I wasn't given the opportunity to present them before the decision was made.

I still hope I can save it.






