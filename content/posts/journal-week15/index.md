---
id: "1234"
status: published
createdAt: 2026-07-19T00:00:00+00:00
firstPublishedAt: 2026-07-19T00:00:00+00:00
publishedAt: 2026-07-19T00:00:00+00:00
updatedAt: 2026-07-19T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week15.png
date: 2026-07-19
excerpt: "A week of tough choices: reducing scope to meet Waad’s deadline, learning how Meta, Google Ads, and LinkedIn manage advertising at scale, and facing the limits of billing and account structures. Meanwhile, an Odoo–Shopify integration reminds me that friction is often a sign that change is finally becoming real."
slug: journal-week-15
title: Journal - Week 15
---
# Journal - Week 13 
	
## Intro

Good morning, one more week. As always, thanks for reading my blog, where I describe the learnings and challenges from the projects I am working on.

This week, I have lots of things to tell you.

Regarding Waad, I will discuss some architectural decisions we have made to speed up development and meet our ambitious deadline. I will also share some interesting findings about how digital advertising platforms allow companies to manage potentially hundreds of thousands of advertising accounts under the same corporate umbrella.

I will also share my learnings from building a production-ready agentic application, which is still very much a work in progress.

Last but not least, I will discuss the Odoo–Shopify integration, the problems I am experiencing with data duplication, and how to calm different company departments when friction arises from adopting a new tool.

## The Deadline and the Scope

As you know, we have a tight deadline. I have already mentioned it several times.

We are also a small seed-stage startup team working at the edge of technology, exploring relatively uncharted paths. Therefore, we do not have enough previous experience to know exactly what we will encounter, which seriously compromises the reliability of our estimates.

And finally, it is summer. People want to take some time off and go on holiday. Bad people! :D

I am therefore revisiting the initial estimates every two weeks. We are fully in implementation mode. Yes, we have AI, but we cannot blindly vibe-code the entire application—or at least we should not.

We have nine weeks ahead of us: a very hard countdown.

Whatever we ship must serve the interests of our business development team and help us gain real traction, but it also needs to satisfy investors.

Tomorrow, I have a meeting with the lead developer to bring the submodules that make up Waad’s main modules back down to earth and try to get a firm commitment from him.

I already have several ideas in mind to reduce the scope even further.

One option is to outsource the UI/UX and the development of the customer-facing application to our marketing agency. They are doing a pretty decent job, were part of the initial brainstorming process, and understand the ins and outs of what we want to achieve. It would be a natural fit, as this is precisely their area of expertise.

I am also considering throwing my soul—and every good practice related to developing production-ready software—overboard and simply vibe-coding the entire application.

Technically, it could be suicide, but it might serve Waad’s very short-term interests. It would probably mean starting again from scratch in October. There is also the risk of something going seriously wrong technically after giving the AI too much decision-making power, leaving us unable to understand or solve the problem ourselves.

I am still reluctant to do this. I want to retain control of the codebase. I want to understand why the models are designed the way they are, why the codebase has its current structure, and why each decision was made.

I will leave the more boring architectural decisions until the end. These could also help us reduce the scope, such as limiting the initial number of advertising platforms included in the first release and keeping the entire administration interface server-side, using a good old HTML template engine such as Thymeleaf, FreeMarker, or even JSP. What memories!

## New Learnings About the Platforms

When we started investigating the foundations of this project, we knew that many black boxes would need to be opened.

One of them was understanding how we could activate advertising campaigns on behalf of our customers—potentially millions of them.

What we discovered was very interesting and changed some of our initial assumptions.

We started by looking at Meta.

Meta has a clear process for advertising on its platforms, although it is naturally conditioned by how the Meta ecosystem works. Meta has its own space on the internet: Facebook, Instagram, and WhatsApp, all interconnected.

Within this ecosystem, companies and individuals create their own pages and profiles. When they advertise, they advertise through these assets.

Therefore, if we want to advertise on their behalf, they need to grant us permission to manage those assets. Everything happens inside the Meta universe.

Google Ads and LinkedIn, however, do not work in exactly the same way.

Google Ads, which encompasses several channels such as websites, search, and display advertising, operates across the internet as a whole. Companies and individuals have their own websites, landing pages, and e-commerce platforms that they want to promote.

Unlike Meta, customers do not grant us access to their assets so that we can advertise through them. Instead, they need to grant us access to their Google Ads account.

Our main target audience is companies with little or no knowledge of digital advertising. For this MVP, we are therefore assuming that they do not already have a Google Ads account and that we will need to create one for them programmatically.

That sounds straightforward enough, but it raises another question: how many Google Ads accounts can we create, and how can we connect all of them to Waad’s services?

Google’s solution is to use a Manager Account, previously known as an MCC account, which can contain and manage multiple customer Google Ads accounts.

However, a single Manager Account cannot manage millions of accounts. Therefore, if the project is successful, at some point we will need to consider a hierarchy in which Manager Accounts contain other Manager Accounts, which then contain the individual Google Ads accounts.

Finally, there is LinkedIn.

LinkedIn is a mixed case. In theory, it could work similarly to Meta because it has its own ecosystem of company pages that can be used as destinations for advertising.

However, in practice, it also has a concept similar to Google Ads: an umbrella platform called LinkedIn Business Manager, which can contain multiple LinkedIn Ads accounts.

The limitations are similar to those of Google Ads, but potentially even worse. LinkedIn does not allow the same hierarchical structure. This means that we may need to provision additional LinkedIn Business Manager accounts as we grow.

It is also unclear whether we can create multiple parallel LinkedIn Business Manager accounts using the same company information.

On top of all this, there is the billing problem.

Currently, we are relying on credit cards as the payment method used to charge advertising costs to companies. However, credit cards have limits. You cannot assume that millions of euros per month can be charged to a single card.

An end-to-end commercial agreement between Waad and the advertising platforms will eventually be necessary. As you know, these kinds of agreements can take months to negotiate.

None of this worries me too much right now. We are currently very focused on September. However, it is useful to keep these limitations in mind so that they do not surprise us later.

## Friction When Introducing a New ERP

In parallel, I am doing a small consulting engagement for an e-commerce company with approximately €4 million in annual revenue, helping them integrate an ERP system.

After accelerating the project, the third-party implementation partner and I started adding more and more shops to the ERP.

This meant that several departments experienced the restrictions imposed by an ERP system for the first time.

We had communicated several months ago that the implementation had started. We had also taken some initial steps with less complicated shops and sales channels.

However, as those departments were not actively using the system, nobody complained.

Now that we are starting to step into their territory, the friction has begun:

“We do not know how to use the tool.”

“There were no workshops!”

“We cannot do what we did before.”

The last complaint is particularly interesting because, in some cases, what they were doing before was systematically incorrect.

However, they are the final users, and we need to listen to them and help them.

In the end, we found some workarounds that made them happy, and we also offered additional workshops. I believe everything has calmed down again.

Nevertheless, I think this friction is actually very good news.

It means that the implementation is becoming real and that we are slowly moving in the right direction.

## Conclusion

Another week of hard work.

I hope some of the topics discussed here resonate with you.

Do not hesitate to contact me if you would like to go deeper into any of them. You can find me on LinkedIn.









