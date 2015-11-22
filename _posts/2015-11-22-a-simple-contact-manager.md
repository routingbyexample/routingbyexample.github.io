---
layout: post
title:  "A simple master/detail contact manager"
date:   2015-11-22 00:00:00
categories: angular2 component-router
tags: angular angular2 component-router
number: 2
minutes: 5
---

In this example we use Component Router to create a simple contact manager.

# Learning objectives

In this example you will learn:

- how to use `router-outlet` to tell the router where to insert content
- how to use `router-link` to activate routes
- how to use the `Router` service to activate routes
- how to map routes to Angular components using the `@RouteConfig` decorator
- how to configure route parameters
- how to query route parameters using the `RouteParams` service

The code in this example is written using:

- Angular v2.0.0-alpha.46
- Component Router v2.0.0-alpha.46

The entire source code is available [here](http://plnkr.co/edit/sWa7LpRO15YvKDu9OzW0?p=preview).

# Preview

Here is a preview of what we will be building:

<iframe class="rbe-iframe--plunk" src="http://embed.plnkr.co/sWa7LpRO15YvKDu9OzW0/preview"></iframe>

# Let's get started