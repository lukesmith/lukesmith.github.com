---
layout: post
title: Naming is hard - why choose codenames
categories:
- Development
tags: []
status: publish
type: post
published: true
meta: {}
author: Luke Smith
---
Everyone knows there are [two hard things](https://martinfowler.com/bliki/TwoHardThings.html) development; cache invalidation, naming things and off by one errors. 

Starting a new project, if you choose the wrong project name it becomes incredibly difficult and costly to change. You're going to be stuck with it forever.

Let's take a hypothetical service called CompanyName.PricingAllocator.

It's descriptive of what it does, as long as that's all it ever does. The moment someone extends it, because it's "quicker" to extend than create a new service, to do something entirely unrelated then the name becomes meaningless if not confusing.

What if, through good intentions, it's named this way originally but after a period of time the company turns around and says "We can't call it that anymore, that's not the valid terminology for what it does and it has to be renamed"*.  There's the cost of changing not only the code repository, references in CI and other tooling but also the humans who are used to referring to it in the old language.

In a microservice world we should be able to build and replace existing services. What do you do if you need to rewrite the PricingAllocator? And please don't suggest NewPricingAllocator.

This is why you need to give your projects codenames.

Puns or tenuous references, items from a set like cities or animals. Anything that is simple, unique across the company and short.

Back to the original example. Referring to the service that allocates prices as Alligator will soon catch on, people will learn what it does and start using it in conversation. The Readme.md should describe in detail why it exists and what it does. It's then easier to talk about than "The Pricing Allocation Service". And when it's time to replace the service, Crocodile can come along and be deployed side-by-side. 

\* this has happened to us recently on a project.  Fortunately we were only a few weeks in to building the service when we were told it needed renaming.
