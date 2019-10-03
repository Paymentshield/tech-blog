---
layout: post
title: Managing Azure APIM with git
feature-img: "assets/img/pexels/desk-messy.jpeg"
thumbnail: "assets/img/thumbnails/desk-messy.jpeg"
image: "assets/img/thumbnails/desk-messy.jpg" #seo tag
tags: [Azure, Microservices, API]
author-id: sg
---

When we decided we wanted to build a new REST API, we made the decision to decompose the backend into separate services as much as was practical. This would hopefully make good use of Azure App Services as an auto-scaling infrastructure, and it would encourage us to decouple the API from underlying implementations - now and in the future. Like many organisations, we're on the microservices journey and this looked like a good start.

To present a consistent API to our integrators (despite the diverse hosts potentially serving up the answers) we needed a facade layer on top. As part of our buy-in to modern Azure services, we stumped for Azure API Management (APIM).

## Azure APIM config with git

You can set up APIM with a load of point and click in the Azure portal. Naturally, this doesn't work well for long term maintenance; we need a consistent, offline, version-controlled method of making changes to the APIM config.

Fortunately, the idea of DevOps isn't lost on MS, who built a git repo into every APIM instance. As a result, you can check out your APIM config from its internal repo, make changes in VS Code or your editor of choice, and sync them back up to the live instance.

This really helped us when it came to duplicating our UAT setup across to Live. Having set up UAT, we pulled it down, and also pulled down the "emptyish" Live APIM repo (in fact, a new APIM instance is bootstrapped with an example 'Echo' API). Knowing that the API scheme was identical across UAT and Live, and only the endpoints had changed, we copied the config across, and then searched for and replaced our known 'UAT' URL segment with the Live URL segment. Then a simple git add, commit, and push later, the config was up in Live with the correct underlying URLs.

The added benefit of controlling APIM config through git is that perhaps not every developer has contributor access to the Live APIM in the portal, but this way you can control access by means of the (time limited) git credentials and extend trust to devs by... giving them those credentials. Easy.