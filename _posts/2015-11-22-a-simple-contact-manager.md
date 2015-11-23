---
layout: post
title:  "A simple master/detail contact manager"
date:   2015-11-22 00:00:00
categories: angular2 component-router
tags: angular angular2 component-router
number: 2
minutes: 6
---

In this example we use Component Router to create a simple contact manager that uses 2 routes:

- `/`: display list of contacts
- `detail/:id`: display form to edit contact with id `id`

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

## The plan

Let's think about what we need to do:

- we must create `ContactsListComponent` to display all contacts
- we must create `ContactsDetailComponent` to display the details of a single component
- we need to define 2 routes:
    - one route that renders `ContactsListComponent`
    - one route that renders `ContactsDetailComponent`
- we need to add `router-outlet` to tell Component Router where to render the components

## Create ContactsListComponent

<aside class="rbe-aside-filename">contacts-list.component.ts</aside>

{% highlight javascript %}
{% raw %}
import {Component, OnInit} from 'angular2/angular2';
import {ContactsService} from './contacts.service';
import {Router, ROUTER_DIRECTIVES} from 'angular2/router';

@Component({
  template: `
    <h2>Contacts</h2>
    <p>Click a contact to edit:</p>
    <ul>
      <li *ng-for="#contact of contacts">
        <a [router-link]="['ContactsDetail', {id: contact.id}]">
          {{contact.firstName}} {{contact.lastName}}
        </a>
      </li>
    </ul>
  `,
  directives: [ROUTER_DIRECTIVES]
})
export class ContactsListComponent implements OnInit {
  public contacts: any[];
  public selectedContact: any;

  constructor(
    private _router: Router,
    private _contactsService: ContactsService
  ){ }

  onInit() {
    this._contactsService.getAll().then(contacts => this.contacts = contacts)
  }
}
{% endraw %}
{% endhighlight %}

## Create ContactsDetailComponent


<aside class="rbe-aside-filename">contacts-list.component.ts</aside>

{% highlight javascript %}
{% raw %}
import {Component,  OnInit}  from 'angular2/angular2';
import {ContactsService}   from './contacts.service';
import {RouteParams, Router, ROUTER_DIRECTIVES} from 'angular2/router';

@Component({
  template: `
  <div *ng-if="contact">
    <h2>{{contact.firstName}} {{contact.lastName}}</h2>
    <div class="form__row">
      <label>First name: </label>
      <input [(ng-model)]="contact.firstName" placeholder="First name"/>
    </div>
    <div class="form__row">
      <label>Last name: </label>
      <input [(ng-model)]="contact.lastName" placeholder="Last name"/>
    </div>
    <div class="form__actions">
      <button (click)="doSave()">Save</button>
      <button (click)="doCancel()">Cancel</button>
    </div>
  </div>
  `,
  directives: [ROUTER_DIRECTIVES]
})
export class ContactsDetailComponent implements OnInit  {
  public contact: any;
  public backup: any;

  constructor(
    private _router:Router,
    private _routeParams:RouteParams,
    private _contactsService:ContactsService
  ){}

  onInit() {
    let id = +this._routeParams.get('id');
    this._contactsService.getOneById(id).then(contact => {
      this.contact = contact;
      this.backup = Object.assign({}, contact);
    });
  }

  doSave() {
    this._router.navigate(['ContactsList']);
  }

  doCancel() {
    this.contact = Object.assign(this.contact, this.backup);
    this._router.navigate(['ContactsList']);
  }
}
{% endraw %}
{% endhighlight %}


## Define the routes

Let's add the route definitions to our main `app` component:

<aside class="rbe-aside-filename">app.component.ts</aside>

{% highlight javascript %}
@RouteConfig([
  {path: '/', component: ContactsListComponent, as: 'ContactsList'},
  {path: '/detail/:id', component: ContactsDetailComponent, as: 'ContactsDetail'}
])
@Component({
  selector: 'app',
  templateUrl: 'src/app/app.html',
  directives: [ROUTER_DIRECTIVES]
})
export class App {}
{% endhighlight %}

## Add router-outlet

Let's add the `router-outlet` element to the `app` component template:

<aside class="rbe-aside-filename">app.html</aside>

{% highlight html %}
<main>
  <router-outlet></router-outlet>
</main>
{% endhighlight %}


