---
layout: post
title: Managing Azure APIM with git
feature-img: "assets/img/pexels/desk-messy.jpeg"
thumbnail: "assets/img/thumbnails/desk-messy.jpeg"
image: "assets/img/thumbnails/desk-messy.jpg" #seo tag
tags: [Azure, Microservices, API]
author-id: sg
category: Development
excerpt: Azure API Management lets us present a consistent view of our microservices APIs, but how can we securely and repeatably make changes to APIM environments?
---

When we decided we wanted to build a new REST API, we made the decision to decompose the backend into separate services as much as was practical. This would hopefully make good use of Azure App Services as an auto-scaling infrastructure, and it would encourage us to decouple the API from underlying implementations - now and in the future. Like many organisations, we're on the microservices journey and this looked like a good start.

To present a consistent API to our integrators (despite the diverse hosts potentially serving up the answers) we needed a facade layer on top. As part of our buy-in to modern Azure services, we stumped for Azure API Management (APIM).

## Azure APIM config with git

You can set up APIM with a load of point and click in the Azure portal. Naturally, this doesn't work well for long term maintenance; we need a consistent, offline, version-controlled method of making changes to the APIM config.

Fortunately, the idea of DevOps isn't lost on MS, who built a git repo into every APIM instance. As a result, you can check out your APIM config from its internal repo, make changes in VS Code or your editor of choice, and sync them back up to the live instance.

![Azure APIM Portal showing Repository Sync status](/assets/img/sg-apim-test.png)

This really helped us when it came to duplicating our UAT setup across to Live. Having set up UAT, we pulled it down, and also pulled down the "emptyish" Live APIM repo (in fact, a new APIM instance is bootstrapped with an example 'Echo' API). Knowing that the API scheme was identical across UAT and Live, and only the endpoints had changed, we copied the config across, and then searched for and replaced our known 'UAT' URL segment with the Live URL segment.


A simple git `add`, `commit`, and `push` later, the config was up in Live with the correct underlying URLs.

The added benefit of controlling APIM config through git is that perhaps not every developer has contributor access to the Live APIM in the portal, but this way you can control access by means of the (time limited) git credentials and extend trust to devs by... giving them those credentials. Easy.

## The trickiness of generated credentials

The generated credentials are not super-easy to use. I found that my git client struggled with them in the usual username/password box, and I had to instead set my remote up using the syntax `https://user:password@repository.url`. To further complicate matters, the APIM Git password contains special characters, so you have to URL-encode it first.

After this rigmarole, the repo works as you'd expect. The last gotcha is that in a month's time, you'll need to remove your remote and re-add it with the new password, as 30 days is the maximum lifespan for APIM credentials!

## What's next

It would be nice if APIM could use a third party repository, like Azure App Services etc can be deployed from Azure Repos or GitHub. Currently we're limited to using this built-in git repo, which as you can see, has its limitations.

If you're working with APIM, how have you solved DevOps?