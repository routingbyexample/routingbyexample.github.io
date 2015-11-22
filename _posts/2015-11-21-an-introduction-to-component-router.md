---
layout: post
title:  "An introduction to Component Router"
date:   2015-11-21 00:00:00
categories: angular2 component-router
tags: angular angular2 component-router
---

In this example we use Component Router in an Angular application to navigate between two pages.

# Learning objectives

In this example you will learn:

- how to load Component Router in your Angular application
- how to use `router-outlet` to tell the router where to insert content
- how to use `router-link` to activate routes
- how to map routes to Angular components using the `@RouteConfig` decorator

The code in this example is written using:

- Angular v2.0.0-alpha.46
- Component Router v2.0.0-alpha.46

The entire source code is available [here](http://plnkr.co/edit/f2SM6AVJTBjL77j81jEA?p=preview).

# Preview

Here is a preview of what we will be building:

<iframe class="rbe-iframe--plunk" src="http://embed.plnkr.co/f2SM6AVJTBjL77j81jEA/preview"></iframe>

# Let's get started

## Loading Component Router

First we load the Component Router library in the `head` section of our application:

<aside class="rbe-aside-filename">index.html</aside>

{% highlight javascript %}
<script src="https://code.angularjs.org/2.0.0-alpha.46/router.dev.js"></script>
{% endhighlight %}

When bootstrapping Angular, we tell it to add the router to its dependency injection system:

<aside class="rbe-aside-filename">main.ts</aside>

{% highlight javascript %}
// Import Angular dependencies
import {bootstrap, provide} from 'angular2/angular2';

// Import Component Router dependencies
import {
  ROUTER_PROVIDERS,
  LocationStrategy,
  HashLocationStrategy
} from 'angular2/router';

// Import application component
import {App} from './app/app.component';

// Bootstrap the application
bootstrap(App, [
  ROUTER_PROVIDERS,
  provide(LocationStrategy, {useClass: HashLocationStrategy})
]).catch(err => console.error(err));
{% endhighlight %}

## Adding router-outlet

We use `router-outlet` in our template to tell Component Router where to insert content in our application.

<aside class="rbe-aside-filename">app.html</aside>

{% highlight html %}
<main>
  <router-outlet></router-outlet>
</main>
{% endhighlight %}

Contrary to what you may expect, Component Router does **not** insert the content in the `router-outlet` element but adds i **right behind** the `router-outlet` element:

<aside class="rbe-aside-filename">app.html</aside>

{% highlight html %}
<main>
  <router-outlet></router-outlet>
  <!-- The router will put the content here, right after the outlet -->
</main>
{% endhighlight %}



# Final result

<iframe class="rbe-iframe--plunk" src="http://embed.plnkr.co/f2SM6AVJTBjL77j81jEA/preview"></iframe>