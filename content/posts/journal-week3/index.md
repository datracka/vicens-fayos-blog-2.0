---
id: "1234"
status: published
createdAt: 2026-04-24T00:00:00+00:00
firstPublishedAt: 2026-04-24T00:00:00+00:00
publishedAt: 2026-04-24T00:00:00+00:00
updatedAt: 2026-04-24T00:00:00+00:00
author_id: "1"
cover_image: images/journal-week3.jpg
date: 2026-04-24
excerpt: "This week brought something different from the usual client work: I delivered a workshop in Logroño on Agentic Architectures — how to build apps powered by agents — to around 30 people from the local IT community. I also navigated two other challenges: helping a talented ML-focused team member get unstuck on a RAG implementation by pairing him with a seasoned app developer, and pushing a client to replace their shared-passwords Excel file with a proper password manager (slow progress, but moving in the right direction)."
slug: journal-week-3
title: Journal - Week 3
---

## Journal - Week 3

### Introduction

Hi there,

this week is a bit different from the previous one. Mainly because this week, besides the daily business of managing the products and projects from my clients, I did a workshop in my city of adoption, Logroño.

> Logroño is a beautiful small city in the North of Spain. Known for being the capital of wine and the most famous wine region in Spain, La Rioja. It is in a valley surrounded by mountains where you can even ski, very well connected, with an airport 1h away (Bilbao).

So, as always, let's start.

### The Workshop

The workshop was about the topic I have been mastering lately: Agentic Architectures, or how to build apps powered by agents.

Around 30 people attended. Logroño has a very small but cohesive IT community. There are a bunch of consulting companies and marketing and IT agencies, enough to have some colleagues and friends to discuss the latest tech trends and hypes with.

The topic, of course, was very well received. We know that everything AI-related is very catchy.

Whenever I do presentations, I like to approach them in a very familiar way. I don't want them to sound pretentious, with lots of acronyms and complex concepts difficult to understand, where the speaker wants to put himself on a pedestal.

On the contrary, I always try to make the difficult easy to understand. After 25 years working in IT, I have to admit I am a bit tired of the kind of people who want to make us think they are smarter than us just by saying sentences nobody understands.

Lastly, after the slides, I showed them a demo. It was a complex one, I have to admit, with 3 services running in parallel locally, showing an end-to-end app. Thanks to Claude Code, it took me around ~15 hours to develop. Otherwise, it would have taken weeks.

### Helping a Team Member

Another challenge not directly related to tech stuff is how to align one of the team members with the short-term goals of the product.

Let me explain shortly what happened. There are several modules / components / services built in this AI product we are developing.

One of them, as it could not be otherwise, is to develop a RAG.

> RAG means Retrieval Augmented Generation, another fancy term but very easy to understand. It is about powering an LLM — which by definition is closed off from the external world from the moment the training finishes — with an external database to provide better context for a use case. Example: you have a chatbot for a company powered by an LLM, but you would like the bot to know everything about the company's product return policy. Then you need to provide the database with the documents related to the bot so it can advise customers properly.

RAG is an engineering challenge. It can be fairly complex. The team member, although smart and seasoned in everything related to machine learning, was having trouble picking up the issues to build the app that holds the RAG. I tried several meetings, demos, and also a detailed step-by-step to-do list. But the point is that, if you have never faced a problem like that before, you need some time until you wrap your head around it in the right direction.

The solution has been to pair him with another team member who, although not proficient in AI itself, has years of experience building apps. I think they will pair extraordinarily well and I am very positive about the outcome. I will keep you updated.

## Consulting a Company to improve security processes

The last topic I'd like to discuss today is how difficult it is to set up processes in a company that has grown fast and anarchically. The task I have been assigned is to help them remove possible security issues. They haven't had any problems yet, but the CEO is very concerned about it.

After a diagnosis, we identified several high-risk points to solve. The very first one we chose — because it could shut down the company from one day to the next, and because it was _easy_ to implement — was to tidy up the company's shared passwords.

Yes, you guessed it: they had (and still have) a shared Excel file where the whole company is able to pick up shared passwords based on their needs. You can easily understand how risky this is: passwords can leak easily. One employee willing to act badly could put the company in serious trouble.

The proposed solution was to add a password manager and name every head of the company responsible for transferring and storing the passwords from the Excel to the tool.

Do you guess what has happened? At the moment, only 2 heads are using the tool in some way, and the % of passwords that are managed by the password manager is still just 10%. Workshops have been done. It was also communicated through the company, but you know, the daily business is the daily business.

Again, I am positive: we are going in the right direction, doing baby steps, although the situation is still far from the desired goal.

### Conclusion

One week more, one week less. It was a fun week, I have to admit. I hope the pairing I commented on above will work, and I am open to doing more workshops in Logroño and, why not, in other cities.

Until next journal, happy life!

> Note: NOT AI-generated at all. I only passed it, after writing, through Claude to correct grammar errors, as I am not a native English speaker. BUT the main ideas and ways of expressing them remain untouched.






