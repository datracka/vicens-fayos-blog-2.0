---
id: "1234"
status: published
createdAt: 2026-06-19T00:00:00+00:00
firstPublishedAt: 2026-06-19T00:00:00+00:00
publishedAt: 2026-06-19T00:00:00+00:00
updatedAt: 2026-06-19T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week11.png
date: 2026-06-19
excerpt: "This week I share three topics that have been shaping my day-to-day work: using Infrastructure as Code to keep documentation synchronized with reality, experimenting with Spec-Driven Development and OpenSpec, and building an acceptance testing architecture to help a small team move faster. Different challenges, but all connected by the same goal: creating systems that scale knowledge, reduce friction, and allow teams to focus on delivering value instead of maintaining processes."
slug: journal-week-11
title: Journal - Week 11
---
# Journal - Week 11
	
	## Intro

Good Monday morning, and thanks for reading my weekly post. This time, I indeed have some great topics to discuss. I started a couple of endeavors that I think are very important.

In my role as an fCTO, I have had the opportunity to manage teams of different sizes, although the ones I feel most comfortable with are the smaller ones. And not precisely because there is more work, but rather the opposite.

In large teams with 10 or 15 engineers, there are usually also POs/PMs, architects, tech leads, and engineering managers, so the management responsibilities are quite spread out. Whether it is managing the backlog, defining the architecture, setting team policies, or mentoring engineers, responsibilities are shared among several people.

In smaller teams, although you have to do all of these things at the same time, I have to say I love all three areas. (Well, okay, I have my preferences: first, I love pushing ideas further and managing projects; second, I love defining the tech stack and architecture of an application; and last but not least, I enjoy keeping team morale high.)

## God Save the IaC

I love IaC. I knew it was the right choice when I asked the team to learn CDK and start developing our infrastructure with it. Terraform or CloudFormation would also have been acceptable, but building infrastructure purely through visual tools was not.

One of the biggest issues in every organization I have had the opportunity to collaborate with is documenting knowledge. It is very difficult. Most organizations do not have enough documentation, and those that do often struggle with keeping it up to date.

The same applies to infrastructure. Of course, the challenges of documenting infrastructure are different from other areas, but it is still important to have it properly documented so the team and other departments understand how things are built internally.

With IaC, this happens almost out of the box. First, because reading the code already provides a good understanding of what has been built. Second, because in the age of AI, building a script or application that parses the code and generates human-readable documentation is relatively easy.

And that is exactly what I have been doing. As a side project, while working on other product-related initiatives, I spent a couple of hours instructing Claude Code to build a script that can be triggered whenever we want. Right now it is a manual process, but it could easily be integrated into the CI pipeline, generate an artifact, and deploy it to a documentation repository.

Each architectural change triggers a documentation update. Documentation and infrastructure remain synchronized in real time.

## Talking About Spec-Driven Development

I have been using Spec-Driven Development (SDD) and one Spec-Driven Framework (OpenSpec) intensively for the last two or three months. There is a lot of hype around it, and I wanted to see whether it was genuinely useful. My conclusion: it depends.

Working with SDD brings more structure to your day-to-day work, makes agents more deterministic, and provides genuinely up-to-date documentation about what the application is doing. It is also very easy to integrate into your daily workflow. There is really no reason not to give it a try.

The two issues I would like to highlight are that I do not see it scaling easily within a large team, and that it does not yet fit naturally into the traditional developer mindset. Developers tend to focus on implementing the _how_, whereas SDD places much more emphasis on defining the _what_ and the _why_. That is a shift toward a PM/PO mindset.

It is precisely in the PM/PO role where I believe this tool can really shine.

In my daily workflow, I write the task in Linear. The agent picks it up and starts implementing it. Then I continue discussing it, updating the generated artifacts, and contributing to the codebase. The related Linear issue is updated accordingly as the work progresses.

Ah, I almost forgot. The whole point of this section was actually to tell you that I had the pleasure, once again, of presenting a topic at one of our monthly events.

## The Role of the Hands-On CTO and Acceptance Testing

Yes, this is the last topic I would like to discuss briefly with you today.

Currently, my role as CTO includes:

- Stakeholder communication
    
- Project management
    
- Architecture definition
    
- Keeping the team motivated
    
    - Translating business goals into technical requirements
        
    - Removing blockers
        
    - Keeping the team aligned
        
    - ...
        
- ...
    

As you can see, it is quite a lot. I also try to delegate as much as possible and bring the business side as close as I can to the day-to-day work in order to help with testing.

Testing is currently the area where I am focusing most of my efforts to support the team. The mandate is clear: we need to automate testing as much as possible. We are a small team, and we simply cannot afford to spend large amounts of time on manual testing. Testing is extremely time-consuming.

Therefore, I am building the Acceptance Test architecture that will support all of our services. It is still a work in progress, but I expect to have it ready for the next sprint.

Until then, enjoy the week!



