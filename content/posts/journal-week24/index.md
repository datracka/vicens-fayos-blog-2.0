---
id: "1234"
status: published
createdAt: 2026-09-18T00:00:00+00:00
firstPublishedAt: 2026-09-18T00:00:00+00:00
publishedAt: 2026-09-18T00:00:00+00:00
updatedAt: 2026-09-18
author_id: "1"
cover_image: images/journal-week24.png
date: 2026-09-18
excerpt: After ten weeks of AI-powered development, our MVP is almost ready. A candid look at faster delivery, failed RAG experiments, architectural trade-offs, and keeping AI-generated systems understandable and under control.
slug: building-an-mvp-with-ai-speed-trade-offs-and-lessons-learned
title: "Building an MVP with AI: Speed, Trade-Offs and Lessons Learned"
---

# Intro

Hi once again, and welcome to my weekly journal.

This time, it is a bit different—not because of the topic itself, which is about the lessons I have learned throughout my career, but because I first want to look back at everything we have accomplished so far and share my honest thoughts about developing with AI.

## We have the MVP—almost—ready

Yes, I am proud to say that. The development work we started in mid-July, according to the GitHub logs, is finally producing visible results. We are still finalizing a few remaining items, but all the services have been deployed and are ready to be tested by the stakeholders and the Product Owner.

In around ten weeks, we have implemented:

- A conversational recommendation engine powered by an agentic application
    
- A multi-platform advertising aggregator connected to Google Ads and Meta Ads
    
- A customer-facing web application
    
- Two back-office applications for managing daily operations
    
- A RAG-based recommendation service—still a work in progress
    

All of this was developed with AI and backed by cloud infrastructure.

Of course, not everything worked as expected. Starting in June, the development team invested heavily in building a RAG-based recommendation engine. It was a big bet. We spent a lot of time discussing the scope of RAG, and the entire team was involved in designing and architecting it while considering our lack of data.

We created hundreds of synthetic datasets and progressed from initial, rather naïve prompt-generated recommendations to a more sophisticated agentic solution built with Semantic Kernel—which we eventually discarded as well.

By the end of June, we began to see that this approach was not producing better recommendations and was consuming too many resources. The surrounding architecture was also very fragile, not production-ready and still required many improvements. As I mentioned in previous posts, I eventually decided to stop the project and pursue a different approach.

I took the lead on the new recommendation engine. It may be less ambitious and is not based on RAG, but it is a fully agentic application powered by frontier LLMs and embedded within our conversational chat—another agentic application.

For this MVP, I believe it is the natural fit. We already had an agentic application for extracting the customer brief, so we are reusing the same scaffolding for the recommendation stage.

We now have six agents working together through deterministic orchestration. And it works.

In the next iteration, we will separate this logic, return to RAG and build an isolated recommendation engine, as we originally intended. It was simply not the right time to build a RAG-based system. That was a valuable lesson.

Apart from this setback, everything has gone largely as expected. The backend and frontend services were delivered on time. We had to reduce the scope slightly in some areas to meet the September deadline, but I think that is fine.

You know the project management triangle: scope, time and people. Our time and available people were limited, so reducing the scope was the only realistic option.

## What AI did to us

I have been actively involved in AI development for the past four months. Very actively, in fact, as I have also helped implement some of the services. In a startup, everyone has to contribute—including the CTO.

Here are my honest thoughts about AI.

Yes, it helps. In my opinion, our development speed increased by around 50%. Everything we have done would normally have required 20 to 24 weeks, but we completed it in approximately 10 to 12 weeks.

That estimate of 20 to 24 weeks assumes we were already proficient in every area involved. But that was not the case.

AWS infrastructure and CDK, for example, were not technologies we had mastered. We had some knowledge and had worked with them on previous projects, but we had never been deeply involved with them. By “deeply involved,” I mean working regularly with a technology for two years or more.

Therefore, AI often followed its own implementation path. Our job was to divide the work into manageable pieces and try to control the AI so that it did not build something we could not understand at all.

But yes, there was a lot of CDK code that we simply trusted.

And I think that is fine. I can say that because I knew where I wanted to go. From previous experience, I knew that an AWS infrastructure based on ECR, ECS, Fargate and Lambda would be more than sufficient.

Perhaps, in the future, we will need a multi-region architecture and will have to restructure and refactor the entire ALB and security-group infrastructure. When that happens, we will need to understand CDK properly because that kind of refactoring will require deep expertise in both CDK and AWS.

But for the MVP and the first product iteration, I think we are good to go. In 2027, we will look for infrastructure specialists to help us.

What I have described is the trade-off we had to accept. In other areas, we did not make the same compromise. The applications and the backend and frontend services are under control. We did not allow AI to build anything we could not understand. We guided it along paths that we already knew were sound.

AI did not make us think less. On the contrary, it pushed us to think more frequently about architectural decisions. We deliberately slowed AI down to keep the product understandable and controllable.

After this experience, I can now estimate much more accurately how long a project built with AI will take. That has been a very valuable lesson.

## Conclusion

That is my post for this week: 24 posts in a row. I am very proud of that. It represents six months without interruption.

But next week, I will be on holiday, so I will not publish anything.

And I think that is okay. Discipline is great—I love discipline—but there must also be room to be lazy sometimes and not feel stressed.

Writing a post every week was not always easy. Although it only required two or three hours each week, I sometimes struggled to find the time. There was plenty to do at the startup, alongside family responsibilities. Some weeks, I had to wake up very early, before the rest of the family, to finish the post.

I am proud of what I have achieved. Next week, I will take a break.

I will be back in two weeks.









