---
id: "194912906"
status: "published"
createdAt: "2023-09-22T14:48:22+01:00"
firstPublishedAt: "2023-09-22T14:48:36+01:00"
publishedAt: "2024-07-04T11:32:25+01:00"
updatedAt: "2024-06-20T12:20:21+01:00"
author_id: "156386009"
cover_image: "images/api.jpg"
date: "2023-09-22"
excerpt: "API first design"
slug: "faster-time-to-market-with-api-first"
title: "Faster time-to-market with API-first (English)"
---

# Faster time-to-market with API-first (English)

A few years ago, I had the opportunity to work in a short engagement with a London startup helping them to build an MVP for one of their latest products. They wanted to trial a strategic partnership with a bigger company within the same sector. The startup would provide a solution for an untapped niche of the market, while the bigger company would act as a catalyst for customers who trust an established brand.

The idea for the MVP was very simple: we had to build a small UI using an SPA framework, and a web service exposing a REST API that would allow both integration with the SPA and with the strategic business partner.

Despite the simplicity of the idea, and although the project had started just a few weeks before I joined, some parts of the project were already a hot mess. In particular around the API.

For starters, we didn’t have actual API documentation anywhere. We had a Google Doc with some notes about the endpoints, and a few examples of the payloads we could expect. The problem was the documentation was very incomplete, half of it was wrong, and it wasn’t maintained.

Needless to say, the API implementation wasn’t tested against the contract, since there was no contract at all! Hence the backend developers were able to release API changes without notice or visibility. Unfortunately, many of these changes weren’t really intended - they were bugs. And sadly, they often broke the integration with the API client. It was frustrating both for the UI developers and for the backend developers.

The second major problem was the backend team wasn’t using a proper API framework. They used plain [Flask](https://github.com/pallets/flask) with custom payload validation which they themselves implemented. You can picture it: hundreds of lines of code dedicated to API validation \(for dates, for timestamps, for string formats, and so on\), most of them untested. No wonder the project was going slow.

To get the project back on track, we had to fix the API documentation, get a proper API framework in place, and make sure no releases were allowed if they didn’t comply with the API specification. Let’s see how we tackled each of these issues.

## Fixing the API design and docs



It turned out the team just wasn’t aware of REST APIs best practices and standards and didn’t know about the [OpenAPI](https://openapis.org/) specification. So the first thing I did was to explain what OpenAPI is and how it works. Then we consolidated the API documentation in an OpenAPI specification. This allowed us to be very clear about what to expect from the API.

The process of consolidating the documentation into an OpenAPI specification also brought to light plenty of problems with the previous API design. For example, dates were being represented with a custom format that required custom validation logic both in the server and in the UI. We replaced those dates with ISO standards, which are [supported by OpenAPI](https://spec.openapis.org/oas/v3.0.1#data-types).

Some schemas also proved to be too flexible and therefore barely useful for validation. In fact, under the name of reusability, the same schemas were reused for different entities, resulting in very **complicated schemas** in which **most properties** were **optional**. To improve validation, we refactored the schemas and created a **one model per entity**, with different endpoints.

Another limitation of the previous design was making **inappropriate use of HTTP methods and status codes**. The only HTTP methods they used were **GET** and **POST**, and all the responses returned **200 status codes**. This wasn’t very useful. The improper use of HTTP methods meant it wasn’t clear when we were trying to create, delete, or update a resource. And since all the responses returned 200, it appeared they were all successful and you had to inspect the actual payload in search for an “error” property to determine whether the request succeeded or not.

From a developer point of view, it may seem like a good idea to “reuse” endpoints. For example, if you capture create, update, and delete operations through a POST endpoint, you’ll have less endpoints to maintain. And if all those endpoints have similar blocks of code, you may also save a few lines. However, you can also do all these things while exposing different endpoints for each operation. This is a common mistake I often encounter among API developers: we **expose our implementation details through the API interface**, and that happens because we think of the **code first**. Instead, I encourage you to **design your API first, and think about the implementation later**.

Consolidating the API specification with OpenAPI was a turning point for the project. From that moment we were able to run **mock servers** to build and test the UI before integrating with the backend, and we were able to **validate the backend** implementation against the specification. We used [**prism**](https://github.com/stoplightio/prism) to run mock servers, and [**Dredd**](https://github.com/apiaryio/dredd) to validate the server implementation \(these days I’d rather use [**schemathesis**](https://github.com/schemathesis/schemathesis)\).

## Fixing the API release process



Having API documentation is very good, but without testing the implementation against the API specification before a release, it’s not much use really. Sure it helps us get a clear understanding of how the API works. But the power of API documentation is serving as a **validation tool** - it helps us verify that the server is correctly implemented.

To ensure the API server worked as expected, I included the **Dredd test suite** in the **Continuous Integration** server, so nobody would be able to merge and release new code unless it was validated by Dredd and therefore compliant with the API specification. Thanks to this, we **stopped having silent changes** to the API server. From that moment on, any changes to the server would have to be documented first, and the API server would have to comply with the changes before merging or releasing.

## Improving the server implementation



The API server was implemented with [Flask](https://github.com/pallets/flask), a popular Python framework for building web applications. Before I joined the team, they’d been using **plain Flask** to build the API, and they wrote a lot of **custom code** to validate API payloads. This is a common mistake I see often among less experienced API developers.

Don’t get me wrong - building your own API validation layer isn’t necessarily bad, but if you go down this route, you’ll end up **reinventing the wheel**. APIs require complex validation logic for both payloads and URLs \(path and query parameters\), and this logic has to be applied throughout the API. So if you build your own API validation layer, you’ll end up creating an API framework. The thing is, there’re tons of API development frameworks out there, and very good ones, so why not use one of them?

When it comes to Flask, in particular, there’re plenty of choices. And in fairness, not all frameworks are created equal. You’ve got [flasgger](https://github.com/flasgger/flasgger), [restx](https://github.com/python-restx/flask-restx) \(successor of [flask-restplus](https://github.com/noirbizarre/flask-restplus)\), [flask-RESTful](https://github.com/flask-restful/flask-restful), and [flask-smorest](https://github.com/marshmallow-code/flask-smorest), to mention a few. How do you choose among those???

When choosing a REST API development framework, you’re looking mainly for the following factors:

- **It supports OpenAPI out of the box**: if you’re going to build a REST API, you need to use a framework that knows how OpenAPI works. Otherwise, you’ll get nasty surprises when it comes to payload validation. The easiest way to determine if a framework supports OpenAPI is by checking whether it can auto generate API documentation from your code. Flasgger and flask-smorest both do this.
- **Uses a robust data validation library**: validating payloads is a complex business. Your data validation library must handle optional and required properties, string formats like ISO dates and UUIDs \(both dates and UUIDs are string types in OpenAPI\), and strict vs loose type validation \(should a string pass as an integer if it can be casted?\). Also, in the case of Python, you need to make sure 1 and 0 don’t pass for True and False when it comes to boolean properties. In my experience, the best data validation libraries in the Python ecosystem are [pydantic](https://github.com/pydantic/pydantic) and [marshmallow](https://github.com/marshmallow-code/marshmallow). From the above-mentioned libraries, flasgger and flask-smorest work with marshmallow.
- **It validates everything**: It validates request payloads, response payloads, URL path parameters, and URL query parameters. I’ve noticed some libraries only validate request payloads and provide very little support for validating URL parameters or response payloads. In those cases, make sure at least the library gives you a way to enforce your own validation rules for responses and URL parameters. If your library uses marshmallow, you can always use the marshmallow model directly to validate a response payload.
- **Maturity**: if your business \(or your job\) depends on the APIs you’re building, you want to build them with robust and mature libraries. Look for libraries that have been around for a while and with lots of users and contributors. Look for libraries with an active community, in which users raise issues often, but check that the issues are quickly addressed. It also helps if the library has good documentation.

After applying this analysis, we chose to work with flask-smorest, which is a Flask plugin that allows you to easily build REST APIs using marshmallow for data validation. This not only allowed us to remove hundreds of lines of custom data validation code - it also improved data validation. Both request and response payloads were now properly validated. Also, while URL query or path parameters were not being validated before, now marshmallow was taking care of all that.

Using a proper API framework was a game changer - it gave us a properly working API. Because the framework takes care of everything in the API layer, we were able to spend less time working on the API layer, and focus our efforts on the business layer and the application’s data model. Our development speed got faster and we were able to release better software more often.



## Moral of the story

APIs are deceivingly simple. At the end of the day, APIs are everywhere and we all use APIs all the time. However, in reality APIs are complex pieces of software. Anyone can build a simple API, but then anyone can also write some random code. Just like the most challenging thing in software development is writing readable and maintainable code, the most challenging thing in API development is delivering good interfaces that work as expected, are easy to consume, and easy to change.

Delivering good APIs is difficult because it requires **alignment with the business**: our API must meet the requirements of our organization. It requires **alignment between the client- and the server-sides** of the API: they must work together and use the same contract, otherwise the integration won’t work. And we must ensure that both the client and the server are **implemented according to the specification**.

Many skills are needed to make this happen: you need to know how to engage with the stakeholders and gather requirements, how to translate those requirements into technical details, how to design an API, how to document it, how to choose a good API framework and how to use it correctly, how to test the API, and how to ensure the implementation follows the design. And this isn’t even considering API security, deployments, and operations. Those too are extremely complex topics, but that’s for another day.

If you’re building business-critical APIs, my recommendation is don’t leave it to your most junior developers on their own. By all means engage junior developers, but make sure their work is supervised by a senior developer who knows how to build APIs. If you don’t have previous experience building APIs, **stick to best practices**: design the API first, document it, build according to the spec, and validate it against the spec. And don’t reinvent the wheel - use proper frameworks!

I know it sounds like a lot of work: you need to learn OpenAPI, figure out how to use API testing frameworks like Dredd and schemathesis, research API development frameworks, and so on. But it’s worth the effort. The alternative is a **downward spiral** of API integrations and software quality problems that will hold your progress back and will cost your business a lot of money to fix.



If you need additional help, reach out to the experts directly \(check previous paragraph\)! Based on my own observations working with different clients and watching many API disasters, I estimate that companies without adequate talent or experience waste somewhere between $50k and $500k trying to get their APIs right. Sometimes it’s way more than that. But money isn’t the biggest problem here: it’s the legacy code that gets built along the way, the burnout among the employees \(who often end up leaving the company\), and the loss of business opportunities, either because the project ships late, or because it gets canceled altogether. So even if you have to pay $50k for a consulting/training session to get things right, you’ll still be much better off: you’ll have saved time and money by getting yourself on the right track from the beginning.

---
