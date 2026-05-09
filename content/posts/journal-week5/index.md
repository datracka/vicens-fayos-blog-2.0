---
id: "1234"
status: published
createdAt: 2026-05-09T00:00:00+00:00
firstPublishedAt: 2026-05-09T00:00:00+00:00
publishedAt: 2026-05-09T00:00:00+00:00
updatedAt: 2026-05-09T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week5.png
date: 2026-05-09
excerpt: |-
  This week’s blog post is about something we rarely discuss enough in tech leadership:

  The emotional side of scope negotiation.

  Building products is not only about architecture, estimations, or delivery plans.
  It is also about listening, adapting, reading people, and finding alignment between business expectations and technical reality.

  After weeks understanding the business, defining modules, and shaping the MVP, we finally reached the difficult conversations:
  What is truly essential?
  What can wait?
  Where is the real red line?

  Sometimes reducing scope is not failure.
  Sometimes it is exactly what gives a project a real chance to succeed.
slug: journal-week-5
title: Journal - Week 5
---
# Journal - Week 5

Intro

Good day whatever the time you read this, and thank you for reading it. 

This week, again important learnings and challenges happened to me. It was at all another routine week where more or less I did, job-wise, the same as the week before. 

I had a complicated meeting with the COO- Product Owner of the startup I am helping to negotiate the scope of the MVP

I was cut hours from one of my clients. 

From technical site, I started the infrastructure in AWS, actually the infrastructure of the infrastructure. 

So, let´s start. 

## Defining the Scope

I am for around 2 months helping an innovative startup to build their product from scratch. The leading team is PRO, good founded and each of the members +25 years of experience in the area. 

So it is not a team of post university friends building the a new idea in an accelerator. 

It has good things, like being good founded and with connections, and not too good things, unexperience in the startup  and the newest trends in the scene.

I am also not a new kid on the block with more than 25 years in IT, yeas I've been hardly coupled to start up scene for the last 15 years but I am not the freshy young anymore that was able to work until late pursuiting the very next unicorn. 

Two months ago, I started getting the business knowledge, no strictly new things as I have mostly related to Marketing and CRM verticals, but more media agencies buying planning related.

I got their vision, I agree, I did not refute anything they had in mind and actually I was signing off the initial and very ambitious roadmap. 

Yep, I over promised I know it is exactly the opposite recommended when scoping a product / project. 

The fact is that, it was so vast the scope of the project (AI Agents, Data Pipelines, Scrapping, Multiple Apps, Queues, third parties integrations among others) that I had that option or just tell them nothing. I had no another option. You know, if you are an experienced tech leader, you have to play with expectations a bit. 

Now 2 months later I have a much cleaner overview what I had on my hands. 

Then the negotiation phase has started. An I am still on it! 

I always do the same, so I guess we can extract some pattern from it

- I gather requirements and write a functional of the WHOLE scope. Nothing written in stone as it can change but, at the time of writing and being signed off by all parts. 
- In parallel I understand deeply the business, what the want to achieve and more importantly WHY.
- I know that in startup, everything, EVERYTHING can change so flexibility is a must, nevertheless we need something to start
- With the requirements gathered, I divid the product in modules, technically speaking. 
- I sort them in the order to be build from technical perspective. Having in mind the resources I have. 
- Also I have in mind not only modules that directly served the porpoise of the product but also all those that are related to non functional aspects / scaffolding. 
- Now I can give a rough time estimation when product iteration MVP phase 1 could be done

But it can be, and usually it happens so, that if I show business the figures and numbers they will not accept it at all. 

Let's say they leave in the world of peter pan where everything is possible and time does not exist :) 

Nevertheless with all this tech knowledge I had the first meeting. 

I explained what would have more sense to build from technical site and if they are happy so. 

I listen carefully and I know that their wishes can not be ignored. Two things can happen. 

Magically tech and business where aligned and there is a high degree of alignment in the proposed timing / scope. 

OR,

They don't understand anything as I start explaining the tech needs and even contradicting myself from the initial agreement. What happened. 

I start negotiating every module, gathering feedback if it could be delayed, mocked, outsourced

From this moment I get what they absolutely need and it is not negotiable. 

The red line.

Once I have the red line I tell them the sentence. 

Ok, let me know go deep on it and I will be back shortly if it is possible and we commit 100% to the delivery or not. 

And in this point I am now. 

Next week I will explain you if I think is possible or not. Spoiler: I think I did a very good job splitting the modules and reducing the scope so I think it is possible. 

Also I will explain you how creativity is very important in this phase. You have to play all the cards you have in your pocket.

So next week, next chapter. 


## Other topics

As I described somerly on the introduction I put the hat of AWS cloud archiitect and start building the meta infrastructure. 

The meta architecture is founded in the following ideas. 

- AWS is the cloud as already mentioned.
- Architecture is built IaaC in CDK and typescript. Everything will be code based with the exception of the user and IAM policies. Those will be defined directly in UI console. I know it would have been also possible, but I don't think we need complicated setups there as we are a small team.
- CI/CD is built based in Github actions.
- Each repo / project / service will have his own infrastructure
- There is also a project for central infrastructure that is cross shared among all services. 

I built the central infrastructure repo, after learning deeply CDK (thanks pluralsight) and using Claude Code. 

Again, AI tools are great but you need to understand what they are building and not blindly hit enter. 

Last topic is a bit of bad news, a client I have just told me he needs to reduce the hours I invest monthly with him due cash issues. I agreed without further negotiation. It is a good client and although I am helping him more as IT tech process advisor than fCTO I have very good learnings about cultural barriers for change, starting from the CEO. 

As always, thanks for reading the post and see you next week










