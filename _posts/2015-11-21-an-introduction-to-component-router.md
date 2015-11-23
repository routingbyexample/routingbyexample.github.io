---
layout: post
title:  "An introduction to Component Router"
date:   2015-11-21 00:00:00
categories: angular2 component-router
tags: angular angular2 component-router
number: 1
minutes: 5
---

This first example is a short introduction to Component Router just to get your feet wet. In later examples we will dive into extreme details, but it's important to cover the basics first.

We will build a simple Angular 2 application that contains a header bar with 2 links. Each link instructs Component Router to display a specific component:

- `/`: display `HomepageComponent`
- `/about`: display `AboutComponent`

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

## Load Component Router

Before we can start using Component Router, we need to load it in the `head` section of our application:

<aside class="rbe-aside-filename">index.html</aside>

{% highlight javascript %}
<script src="https://code.angularjs.org/2.0.0-alpha.46/router.dev.js"></script>
{% endhighlight %}

Next we pass the router providers to Angular's bootstrap function to make sure we can inject the router anywhere in our application:

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

That's it. We have now activated Component Router. But we haven't passed it any instructions yet. So let's do that now.

## Configure the routes

Now that Component Router has been loaded, we need to tell it which routes we want to map to which components.

We can do this using the `@RouteConfig` decorator:

<aside class="rbe-aside-filename">app.component.ts</aside>

{% highlight javascript %}
@RouteConfig([
  {path: '/', component: HomepageComponent, as: 'Homepage'},
  {path: '/about', component: AboutComponent, as: 'About'}
])
{% endhighlight %}

`@RouteConfig` is a component decorator that we can put above any Angular component. It allows us to send an array of route definitions to Component Router.

Let's zoom in on one of the route definitions:

{% highlight javascript %}
{path: '/', component: HomepageComponent, as: 'Homepage'}
{% endhighlight %}

This route definition tells Component Router:

- when the url in the browser changes to `/`, load the `HomepageComponent` component
- export the route as `Homepage` so we can activate the route programmatically using the string `Homepage`
- when the route `Homepage` is activated programmatically, update the browser url to `/`

Now that we told Component Router **what** to render, it's time to tell it **where** we want it to render the component.

## Configure the viewport

We tell Component Router **where** to render content by adding a `router-outlet` element to our template:

<aside class="rbe-aside-filename">app.html</aside>

{% highlight html %}
<main>
  <router-outlet></router-outlet>
</main>
{% endhighlight %}

Contrary to what you may expect, Component Router does **not** render the content inside the `router-outlet` element but **right behind** the `router-outlet` element:

{% highlight html %}
<main>
  <router-outlet>
    <!-- the content will NOT be rendered here -->
  </router-outlet>
  <!-- the content will be rendered here -->
</main>
{% endhighlight %}

Any content that you put inside `router-outlet` will remain visible:

{% highlight html %}
<main>
  <router-outlet>
    <!-- this will remain visible and will not disappear -->
    Loading...
  </router-outlet>
</main>
{% endhighlight %}

Now that we told Component Router where to render content, let's add some links to activate different routes.

## Add links to activate routes

Let's add a navigation bar with links to activate the different routes from within our template.

We use the `router-link` directive on our HTML anchor links to activate routes:

<aside class="rbe-aside-filename">app.html</aside>

{% highlight html %}
<ul>
  <li>
    <a [router-link]="['/Homepage']">Homepage</a>
  </li>
  <li>
    <a [router-link]="['/About']">About</a>
  </li>
</ul>
{% endhighlight %}

The `router-link` directive accepts an array of instructions.

In later examples we will dive deeply into the meaning of the array. For now we just pass an array with a single string representing the route name we want to activate:

{% highlight html %}
<a [router-link]="['/Homepage']">Homepage</a>
{% endhighlight %}

When clicked, the link will activate the route called `Homepage`, which is a route we configured earlier using the `@RouteConfig` decorator.

# Final result

The result is a very simple application with a header bar that contains 2 links.

Clicking a link updates the content accordingly:

<iframe class="rbe-iframe--plunk" src="http://embed.plnkr.co/f2SM6AVJTBjL77j81jEA/preview"></iframe>