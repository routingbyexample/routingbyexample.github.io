---
layout: post
title:  "How to create a single viewport using Angular and Component Router"
date:   2015-11-21 00:00:00
categories: angular2 component-router
tags: angular angular2 component-router
---

# Goal

In this example you will learn:

- how to load Component Router in your Angular application
- what a `router-outlet` is
- how to map routes to Angular components

The code in this example is written using:

- Angular v2.0.0-alpha.46
- Component Router v2.0.0-alpha.46

# Let's get started

## Loading Component Router

First we load the Component Router library in the `head` section of our application:

{% highlight javascript %}
<script src="https://code.angularjs.org/2.0.0-alpha.46/router.dev.js"></script>
{% endhighlight %}

and then we tell Angular to add the router to its dependency injection system:

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

# Final result

<iframe class="rbe-iframe--plunk" src="http://embed.plnkr.co/f2SM6AVJTBjL77j81jEA/preview"></iframe>