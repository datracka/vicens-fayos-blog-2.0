---
id: "1234"
status: published
createdAt: 2026-04-30T00:00:00+00:00
firstPublishedAt: 2026-04-30T00:00:00+00:00
publishedAt: 2026-04-30T00:00:00+00:00
updatedAt: 2026-04-30T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week4.png
date: 2026-04-30
excerpt: "Another week building AI products made one thing clear: SaaS alone is not enough—data is the real differentiator. While interfaces and LLM features are easy to replicate, unique data is not. Building it is harder, less visible, but ultimately what creates lasting value."
slug: journal-week-4
title: Journal - Week 4
---
# Journal - Week 4

## Intro

Hello everybody once again,

One more week of deep learnings. This is why I love being part of a greenfield project in a startup. You never stop learning, and the learnings are significant.

I’m not saying you don’t learn in mid-size or big corporations. I’ve been there and I know it’s true. But you cannot compare—the number of battlefields you face when trying to build the next Shopify, Miro, or X is overwhelming.

So let’s start.

## Everybody is building a SaaS. But stop and build data.

You’ve probably heard it already, and surely you know someone who approaches you with the next $1MM SaaS product they built in 3 weeks.

The reality is much more disappointing.

I won’t go into how difficult it is to make a product successful, even if it’s a good one. Huge—really huge—marketing efforts are required to position a product out there.

But even avoiding that topic, in these times more than ever, a product is not just a nice UI/UX powered by some LLM backend logic. Accept that—many use cases are already covered by the big players. You have the best travel recommender? Claude does that too. You have a cool tool that draws dishes from a restaurant menu so you can see them? Nano Banana already does that. (This is from a video I saw on the Sequoia AI channel, by the way.)

The only real differentiator is data. You need data, and if you don’t have it, you need to produce it.

And building data is much less engaging than building a SaaS frontend.

## How to build a product. Exploring business lines

You may already know that one of the projects in my current portfolio is building an innovative AI-based (SaaS?) product.

And yes, the first thing that comes to mind is a landing page where users can select packages, authenticate, and enjoy the app. Very end-user focused.

But when you build a real product, it’s usually made up of several parts that have value on their own. One of the things I enjoy the most is identifying monetization opportunities and helping businesses rethink their priorities to move—without ignoring investor needs—toward what could be more beneficial long term.

I can’t give too much information due to NDA, but the product I’m collaborating on has at least 3 or 4 monetization approaches beyond the obvious one.

### Team at 100% speed

For me, it’s an obsession that the team is always performing at its best. This, together with having a clear direction so every building block is a step forward, are the two things that matter most to me.

Because I can’t control much more than that.

On the other hand, I strongly believe in having a central document—“The Functional”—that aligns business and IT as the single source of truth. Everybody approves it and builds on top of it.

But sometimes having a finished document, even for the first iteration, is not easy. Too many black boxes, unknown scenarios, and paths to explore to define everything clearly.

The functional document is usually written by the CTO, PO, and other leadership roles, which can delay implementation. If that happens, stop—just build the backbone, get approval, and start building. Perfection doesn’t exist, and the team cannot be blocked.

## Being resolutive

This week I had my first on-call experience with this client, and it was a success. Being resolutive is critical.

This was actually one of the criticisms I received when I was a young manager. My boss liked me—we still have a great relationship—and he was one of my mentors. I still use many of his practices daily. But he once told me I wasn’t resolutive, and he was right. When something technical needed to be solved, I relied on others. I tried to stay in the “manager lane”… young and naive.

This week, around 9 pm, I got a message: the landing page was down. It was built before I joined. At the same time, I learned that the person responsible for it—let’s call him Mr. D—had been dismissed. Two days later, the page went down. Guess who they called? Yes, me.

I didn’t know exactly where the website was hosted. I knew the codebase because I had pushed to centralize everything in GitHub, but hosting—no idea.

So I checked the DNS, found the IP, asked who managed that server, and confirmed it was on OVH. I had access.

Everything looked fine. I logged in through an invoice reference, found the hosting, restarted the service… it didn’t work. I knew it wouldn’t be that easy.

Then I asked the external team who built the site. They told me they had given everything to Mr. D. I couldn’t reach him, so I was stuck—until they kindly sent me a .pem file to SSH into the server.

I logged in, located the app and its Docker containers.

From there, it was fairly simple. I restarted the container and… everything worked again.

## Transfer the data

The last thing I want to mention is how painful knowledge transfer can be when someone leaves and there was no real effort to do things properly.

I had to act like a detective. I didn’t enjoy that part—taking ownership of dozens of accounts, changing MFA access, etc.

I can’t stress enough how important organization is—but we all know the reality:

- There are always time pressures and knowledge gaps  
- Management is often not aware or doesn’t prioritize it  
- Things are done poorly  
- People leave, new ones join, and inherit the problem  
- Management then sees the risk when access is lost  
- But no matter how many times it’s said, it happens again  

Human nature, I guess.

## Others & Closing

Not everything was difficult. I also completed a Single Sign-On migration for a multi-shop Shopify eCommerce company (15 shops) without major issues. I also cleaned up roles and enabled MFA for everyone. I hope it helps improve security.

And after several attempts, we finally regained control of a dozen Meta assets that had been lost due to poor credential management.

That’s all. I hope you found it somewhat interesting.

Have a great (long) weekend!



