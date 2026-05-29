---
id: "1234"
status: published
createdAt: 2026-05-29T00:00:00+00:00
firstPublishedAt: 2026-05-29T00:00:00+00:00
publishedAt: 2026-05-29T00:00:00+00:00
updatedAt: 2026-05-29T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week8.png
date: 2026-05-29
excerpt: |-
  What happens when a company loses control of half of its Facebook and Instagram presence? This week I share a real case where years of poor organization turned Meta assets into a maze of duplicate accounts, inaccessible Business Managers, and lost ownership.

  I also explain why I prefer adding constraints instead of policing teams, and how I use sub-milestones to keep AI projects on track without relying blindly on Agile ceremonies.

  A few practical lessons on organization, leadership, and project delivery from the trenches of IT.
slug: journal-week-8
title: Journal - Week 8
---
# Journal - Week 8

## Intro

Hi everybody from the warm summerly Spain. Yes, one week more sharing my IT adventures and hoping it help somebody else. 

This week I'll talk once again about the importancy of having control of your organization digital assets. 

Also, I'd like to share some organizationals improvements I added to be sure team is following a minimum standars and how I am managing the AI project I have on my hands.  


## It's really too hard being organized?

Let's imagine once of those companies from before the digital era. You know the classical company Mad men style with archives, folders and files. Everybody knew that a company to run, besides what they do better they needed to organize the files correctly, to number them etc.. nobody can Imagine a succesful company with folders and sheets on the ground being stepped over by the employees.

But digitally I see that every time I visit a company. It can be because digital assets are not too easy to visualise as the physical ones, but it is not an excuse. 

Let me explain you the last case I have seen. A small consultancy to a company willing to organize their Meta Ads Accounts. They do Ads in digital space, basically in Meta (Facebook and Instagram) because they rely in community for advertise their products. 

They approach to me because they did not have control aymore about ost of their assets in Meta (Facebook Pages and Instagram accounts). 

After a couple of days autdit I find the following. They have around 20+ FB and IG pages or each of the products / brand they sell. 

Those FB accounts are 30% controlled individually by CEO FB profile but also they have around ~20 Meta Business Managers, each o them managing one of the assets. 

From those Meta Business Managers they have only access to 50% of them. 

The rest they don't know who did, when. They don't know even the accounts / profiles related to those Business Managers. 

Actually, when they found this issue in the past they just pushed forward, duplicating assets and Business Manager. 

For a company the expectation is to have a business manager that acts as umbrella for all the Meta assets... they have ~20.


> Just for your understanding. Meta has a very complicated way to organize assets properties. First you have profiles that can hold FB and Instagram accounts and also Company Pages individually. Then you have the business manager / business portfolio that manages also those assets(like the Company Page) not for managing the content BUT to publish ads on the behave this company Page.

As result of that they can not publish the 50% of the products on Meta. 

A real chaos. I can understand at the beginning you want to grow, you are few people, just the CEO and a bunch of very trustable employees, focused in attract clients. To organize things is secondary...but once you have a bit of structure? Just ignore the issue and kick forward? 

OK, now they have a big issue that is lasting them to grow even more.

Solution to this? very hard. As they don't have a clud about anything related to the 50% of their presence in Meta they need to contact support and for each Business Manager show they are the company behind it.

It will take months to solve it, if they solve it. Still unclear to me. At least know they have a good picture about what they own and how is organized. 

## Don't tell them what not to do, just constraint them

Yeah, when you have a team o people, you can not control what they will do. You have to accept that some things will done in a good shape and other can be just done wrong. 

I don't like, and also I don't recommend, to be babysitting them, telling them what they can do and what not. It is frustrating and it does not work.  It is much much better to add constraints. 

But ok, let's stop about theory and let's go to the practice. 

You know github, a code repository. It can be used in several ways. There are good practices. Not each developer follow them. also sometimes those approaches add more workload and problems that the ones you want to solve. 

So, we have to be very careful what we want to restrict. For the current team after a careful thought I wanted to keep things simple so I just the following. 

- I created a Github template with the repository structure we want to follow. Separating `infrastructure` and `acceptance-tests` from the source code itself
- Add some rulesets to avoid pushing to main and forcing going through PR. 
  
As we are few devs and we communicate pretty well, I removed by now to have CR approvals to merge. I am not pretty sure about it but I don't want to prevent to deliver code because people is waiting for a PR. Also, I know what is happening, CRs are done as favor without looking the code, just as a bureaucratic check... and then they make no sense.

## Milestones under milestones

Last topic I want to talk to you this week is how to track a project to be sure it will be a success. We do have for the AI product we are developing a clear roadmap and a commitment. 

How to be sure we will reach the goal and we deliver the MVP the agreed date. 

We can not rely in agile methodologies and Sprints they are not thought for it, they just worry to keep team deliverability and quality at most but not to align to a date. 

So usually I have sub milestones. They main milestone is to deliver in production the MVP v1 but the submilestones is to deliver on the right time all the submodules. I have identified several sub-milestones and I will track the team. If I see we dely on some o them red flag.

I mean, I am not explaining you anything you don't already know, I do the same thing every morning when I want to bring my kids to school. They wake up, they have to be on table with breakast at 30', put shoes and brush teath at 45' and go at 50' if any of those milestones are broken we know we will go late to school. 

The important message here is, don't rely in tooling and methodologies to much. Usually they are to hide real output, to self explain themself but not to add real value. I am not saying don't use them, but don't forget they are magical. 

## Conclusion

And this is for this week. I just want to wish a very nice start of the week. This one I am meeting some friends from my expat times in Germany so I think I will have time to disconnect a bit from the daily routine. 















