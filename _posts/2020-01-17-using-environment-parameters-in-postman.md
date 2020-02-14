---
layout: post
title: Using Environment Parameters in Postman
feature-img: "assets/img/headers/postman.jpg"
thumbnail: "assets/img/thumbnails/postman.jpg"
tags: [Postman, API]
author-id: nc
category: Development
excerpt: Postman is great for quick API tests. But can we get even quicker by saving time with environment variables?
---

Postman is great for quick API tests. But can we get even quicker by saving time with environment variables? I'm Nick, I'm a software development intern here at Paymentshield, on placement from Manchester Metropolitan, and I'm going to talk a little about how we can use this powerful feature!

## What is Postman?

Postman is an API (Application Programming Interface) development tool which helps to build, test and modify APIs. In Postman, you can  make various types of HTTP requests (GET, POST, PUT, DELETE, PATCH), save environments for later use, and convert the API to code for various languages (like JavaScript and Python).

## What is an environment, and why use them?

An environment is a set of variables that allows you to switch the context of your requests.  Environments are useful as they allow you to create robust requests that you can reuse; by storing values in variables, you can reference it throughout your collections, environments and requests – and if you need to update the value, you only have to change it in one place. This increases your ability to work efficiently and minimize the likelihood of error.

## Setup

To add environmental parameters to Postman, first we have to create an environment . To do this, click on the cog wheel located near the top right of the application (highlighted in yellow below)

![Click the config button](/assets/img/postman/config.png)

After you click the cog wheel, an overlay called "Manage Environments" should appear. Click on the Add button.

![Click on Add](/assets/img/postman/add.png)

Provide an environment name (like Development), and then enter the variable information you want in  this environment. Once you are finished entering all your variables, click Add.

![Set the environment variables](/assets/img/postman/env-variables.png)

After you have added the environment, close the "Manage Environments" overlay and then click on the dropdown near the top right. Change the environment to the one you just created.

![Choose the environment you just made](/assets/img/postman/pick-environment.png)

On a new request, navigate to the Headers tab. Enter your key, and for the value you want to surround the variable name with two curly braces, for example: {% raw %} `{{userid}}` {% endraw %}

 > Tip: entering a curly brace into the value box will display to you the possible variables to use in the environment.

![Use your variables](/assets/img/postman/use-variables.png)

Do this for all of the `key:values` that you need in your header.

Alternatively, you may want to use the Bulk-Edit feature. To add your `key:values` this way, click on "Bulk Edit".

![Click bulk edit](/assets/img/postman/bulk-edit.png)


You can enter your key value pairs in here by the syntax: `key:value`. When using variables as your value, you must wrap the variable with two curly braces, like {% raw %} `{{userid}}` {% endraw %}.

![Bulk editing headers](/assets/img/postman/bulk-editing.png)

Enter the API URL and then send your request.

One last tip: Quickly set your variables from the data in a response body by highlighting the data you want to be stored in an existing variable, right clicking it, and selecting the environment and variable name, as pictured below. This will update it everywhere you've used the matching variable.

![Save body value](/assets/img/postman/store-value.png)


## Wrap up

Hopefully this quick guide has helped you with learning a bit more about:

 * What Postman is and why we use it
 * What environments are and why we should use them
 * How to setup your environment
 * How to actively apply environment variables within your requests
 
Thanks for reading!
