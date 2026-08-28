---
id: "1234"
status: published
createdAt: 2026-08-22T00:00:00+00:00
firstPublishedAt: 2026-08-22T00:00:00+00:00
publishedAt: 2026-08-22T00:00:00+00:00
updatedAt: 2026-08-22
author_id: "1"
cover_image: images/journal-week20.png
date: 2026-08-22
excerpt: "This week: why WordPress can still be the right choice despite more modern alternatives, and how I evaluated adding Vaadin Hilla to our Java stack. Two different decisions with the same lesson: the best technology is not always the newest one, but the one that fits the context best."
slug: journal-20-wordpress-rules-and-new-tech-to-stack
title: Journal 20 - WordPress Still Rules, Adding a New Technology to the Stack
---

# Journal 20 — WordPress Still Rules, Adding a New Technology to the Stack

## Intro

Hey everybody, and a warm welcome to my weekly journal, where I share the experiences, learnings, and challenges that have happened to me during the last week.

This time I want to talk about two topics. The first one is related to a partner-vetting process I was involved in to help the marketing team. It is not strictly related to the process itself, which was not led by me; my role there was as a technical advisor. It is more about how partnering with the best technical solution is sometimes not enough.

The other topic comes from my hands-on CTO position at Waad and the process I followed to select a new technology for our tech stack. Nothing fancy, just something any professional in the same situation faces from time to time.

## Selecting a Partner: WordPress vs Strapi

As I told you in the intro, we started a process to select the agency that will help marketing build the new Waad website.

You know, a company/product website is a very common use case, something that has had plenty of good solutions to choose from over the years.

We did not go for online website builders like Webflow or Wix, or directly for AI. Our marketing department is not so fancy, so the request was to use a good old CMS. And you guessed it, the one they had in mind was WordPress. They know how to use it, and they know it fulfills their needs.

While we were vetting the partners, some of them suggested using another one: Strapi. Strapi is a more modern CMS, a headless one to be more specific. It uses modern technologies, a real SDLC (the one around WordPress was quite sad when I was dealing with it in the past; I hope they have improved), and a static build mode that improves performance and security.

Also, although it does not have the plugin ecosystem of WordPress, for 90% of use cases it has enough out there.

So, on paper, Strapi is better than WordPress... but is that the reality? Nope.

Strapi is great and better than WordPress in some areas, but not enough.

Technically, it is true that it is more secure and offers better performance, but there are workarounds to achieve similar results with WordPress. And everybody knows WordPress, so why should they learn a new stack? Also, WordPress developers are cheaper and easier to find. And the WordPress tech stack, although old, is definitely not dead yet.

So that's the thing: there is no real reason to move away from WordPress, and it is not all advantages.

Therefore, I think that for the use case of building a company website, betting on another CMS instead of WordPress is probably a losing bet.

### Building the Admin with Vaadin

You know that we are building a service that is internally powered by an agentic application as part of our Waad product.

The agentic application is a recommendation engine orchestrating agents and a RAG, and all this powerhouse also needs a back office.

The service exposes a REST API that can be consumed by any client. Should the back office also be a client? That was the very first option the lead developer suggested.

But I was reluctant to go that way, as I thought it would bring extra work for no real benefit.

Why did we need to build a separate service hosting a Next.js app? It means more infrastructure to maintain and, if we talk about application complexity, we need to keep an eye on keeping the UI state up to date and also on the additional layer of having a separate middleware backend, or "lean backend" as some people call it. It allows us to keep all sensitive information (tokens, secrets) server-side, but we have less transparency about what is happening in the flow from the backend service to the browser.

I knew I wanted to build this admin back-office tool server-side. I really thought that the good old approach of having an MVC template-based framework would suffice.

The frontend developer, though, told me he did not want to maintain HTML templates; he wanted to work with components (React or a similar JS library). I accepted this counterargument. In the end, building with components allows us to reuse a lot of code. I also like the "reactive" or publish/subscribe model, as I like to call it. It makes it easier to build UIs with complex states, although that should not be our case!

So the next thing that came to mind was to have an embedded "Frontend Node.js" project inside my Java Spring/LangChain4j service. You know, I could locally run both servers, backend and frontend, during development and build a CI pipeline that provides the transpiled JavaScript code as assets for the Java project to serve.

It solves the problem of duplicated infrastructure, and we still have React in place.

But it was still not perfect. It meant building a dedicated REST Admin API to be consumed by this back office.

Then Vaadin came to the rescue!

I will not go too deeply into what Vaadin is; you can read about it yourself. But basically, it allows you to have a frontend application embedded in your Java project, similar to what I was describing above.

But with two nuances.

First of all, it comes in two flavors. One of them lets you write all the frontend components in Java (Vaadin Flow). I did not want that because of the developers' request.

The second one allows you to write the frontend with React. A nice one. It is called Vaadin Hilla.

The cool thing about Vaadin Hilla is that it generates the API automatically from the services implemented in Java, so you don't have to worry about building a dedicated Admin REST API. Also, the backend logic remains server-side, so it is secure.

Of course, all this magic has a price. For an easy and non-critical UI like this one, it is more than fine, but for very complex setups I am sure that sooner or later I would face limitations.

Nevertheless, for the use case I had in my hands—an internal back office—it was more than good enough.

Of course, it requires understanding the framework properly, and we are adding a new dependency to the stack. I know. But I think it fits our needs very well, so after some thought, I decided to give it the go-ahead.

I will keep you updated on how it goes.

## Conclusion

That's all for this week. As you can see, working at a startup is quite interesting. There is always new stuff to worry about and a very diverse range of topics.

Anyway, I hope that my learnings from this week are useful to you and perhaps serve as inspiration for some issues you may be facing now or in the future.

I wish you a nice start to the week








