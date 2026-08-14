---
id: "1234"
status: published
createdAt: 2026-08-14T00:00:00+00:00
firstPublishedAt: 2026-08-14T00:00:00+00:00
publishedAt: 2026-08-14T00:00:00+00:00
updatedAt: 2026-08-14
author_id: "1"
cover_image: images/journal-week19.png
date: 2026-08-14
excerpt: "This week: the human side of pushing an ERP transformation forward, dealing with resistance to change, and why friction can be a sign of progress. Plus, lessons from building an agentic app, where a small communication gap exposed an important architectural risk."
slug: journal-week-19
title: journal-week-19
---

# Journal — Week 19

## Intro

Hi one week to my weekly digest of learnings and challenges as fCTO. This week I do have interesting topics and this time I will start from an small ERP implementation consultancy that I am leading. It shows the complexities of pushing forward a cross department project and the reluctance of the company teams to the change. 

After expect an update in the challenges I have experienced building the backbone AI agent based app I am leading for Waad.

## Fighting with reactiveness and reluctance to change

This is the situation. an eCommerce company wants to implement an ERP to streamline the processes and gain in productivity. Nothing new at the moment. 

And it has been received with long faces creating lots of friction. Nothing new. 

So how we deal with employees reactiveness and passivity? 

I have to admit I can barely handle those kind of behaviors. In my opinion it is infinitely much worst than directly challenging the implementation. 

Challenging is completely fine and if somebody stand up and openly says to me that X or Y are wrong I am all ears. Most probably it will be very good learnings and, after some exchange of opinions, we will find a common agreement that will help even more the success of the project. 

But this is the exception, usually once you present something like it, you get silence. Comments will be done on close doors, not directly. 

Some teams will try to protect themself using classical "corporate" strategist: We need A and B first, we need workshops, we don't have time enough to do it and of course, blaming the ERP integration as the reason of any delay or malfunction of something that previously worked well. 

For me the very first step has been align the board, I was very clear with it. I can take the leadership and make it happen but I need that is clearly communicated that the project has high priority and that everybody works towards it. 

Also, you need a lot of patience. As I know is the normal behavior and I was the one initiating the project knowing what would happen, I have to help them. Preparing workshops, sending very detailed run books etc etc. I know they do not appreciate it and only are feeling the pain to have to change things the way they were doing previously, but all good.

I am very convinced the gains of finishing the project will be huge and the friction that we are feeling is a very good sign. 

Actually I would raise that a company were there is not friction at all is not progressing. 

## Building an Agentic App

Fine now let's talk about easier things: computers.  - you know the saying: dealing with people is much more complicated than computers \:D 

So, I worked hard moving forward with this app. 

Last week I had already a first version that was exposing a recommendation agent. It did the whole flow. Interviewing the customer, extracting relevant information and proceed with a recommendation. 

So I had the brain. But for testing it only was possible through a rudimentary REPL. So this last days I have worked building the REST Api that will allow to use the recommender from any caller. The recommender builds on a conversational chat as it is the standard nowadays. 

A chat is real time so first thing I had to clarify if with which technology should implement it. My first choice was using SSE Rest API but also I explored alternatives ways like web-sockets and reactive programming.
 At the end I kept the initial though, the other path added unnecessary complexity by now. 

In the meantime of building the REST API I had to deal with others issues, like bugs I found, model improvements, adding JWT validation and the most important of everything align with the rest of the team, in the public façade. 

Here is where the main learning comes. For one of the service that we are building the one that contains the `customer record` the developer had decided to build a relation between customer and users. So, a customer / company can have several users. 

This is a defensive functionality. It is a signal of seniority. You know features that will be requested before they are requested and they build the scaffold first to avoid having to go to painful refactors later on. This was one of them, fair enough. 

But i was not aware, I remember that was part of a conversation and It is in the tech document / functional of that service but I had forgot and also I thought it was not needed. 

false. My service does not know anything against the customer record and we don't want to connect those 2 service 1 to 1 in the MVP to reduce complexity. Therefore an authenticated user could eventually overwrite another customer as I am not able to relate the user to the customer and add a constraint. 

We were discussing what to do and we found an agreement that works, I filled the usual ARD and we move forward but the thing here is that communication failed. This time nothing happen but you see how important is keeping internal and external communication

## Conclusion

that's all for this week, as you can see this week was most human centered than others. Even the Agent AI topic. I hope it reached you and looking forward your comments or suggestions. As always you can reach me by linkedin. 