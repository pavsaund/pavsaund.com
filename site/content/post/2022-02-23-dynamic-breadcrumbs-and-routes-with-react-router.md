---
layout: blog
draft: true
title: Dynamic breadcrumbs and routes and child routes with React Router v6
date: 2022-02-23T21:56:56.732Z
coverSize: partial
thumbnailImagePosition: ""
tags:
  - frontend
  - react
  - react-router
  - routing
categories:
  - DevDiary
---

When faced with a challenge of implementing breadcrumbs for a business critical application recently I went down a rabbit hole of trying to understand the semantics of react-router and finding a good way of building a breadcrumb component that didn't break every time a route was added or changed. Let alone need to implement a custom route for every new page. So let's dig into how I went about solving this...

## The requirements
- Maintain a single routing model (or composition of models) as the source of truth for the app
- Support child routes
- Use the same model to generate bread crumbs for the currently active page.
- Be able to show dynamic breadcrumb title based on parameters.
- Bonus: Support generating Navlinks

## TLDR;
You can check out this github repository to see my trail and error: https://github.com/pavsaund/react-routing-model/

You can view the code in action on stackblitz: https://stackblitz.com/github/pavsaund/react-routing-model/

You can jump over my learnings and use the use-react-router-breadcrumbs package from [XXX]: https://www.npmjs.com/package/use-react-router-breadcrumbs

So, digging into details

It took me a while to really grok the routing model with nested routs in react router v6, even though it was quite straight forward. I put this down to coming from very basic use of v5 and mostly using other frameworks. I found this article on nested routes https://ui.dev/react-router-nested-routes

Based on this I realized I wanted to define my routes as a single model, where possible and to use the `<Outlet />` component to render the routes for a given path.

So I started with the model I wanted, which was built separate from React router's. The idea being that a simple model that can easily be parsed and mapped into something react router could understand. I didn't want to implement ALL the features of react router, but just enough for my use case. This worked fine for my proof of concept

Then after experimenting a bit and also understanding more of the route model that react router expected I actually ended up augmenting what it already expected with a few custom properties. Like this.


Now, for the fun part - actually understanding how to get the active path from React router. This is where grokking how react router builds its path's was important. I realised after hitting my head on the wall that there is no central place where all the routes are stored that is exposed through public api. (Insert note on UNSAFE CONTEXT here). But React Router and nested routes seem to work by each level of the router owning it's own routes and the next level to take over. Meaining that a parent route doesn't actually know anything about it's children, and a child only knows its own path pattern based on the resolved parent's route.

So long story short, each router operates on it's own level and passes its matches along to the next router as the pattern is matched. There's slight more to it to this, as there is a weighting/scoring model involved to assess which route's should win - but that isn't too important at this time.

What I ended up doing was to basically iterating over the route object model to build up the model that was expected, and used the `match` utility to assess if the route pattern is on the active path. Doing this recursively it was realtively straight forward to build a an active path hierarchy that resolved like so.

Now, using the `nav` property on the RoutePathDefinition I could also build up the nav menu for non-parameterized paths like so:

Now I haven't spent much time on the cutomization of the nav-menu, but for my simple needs, this will suffice :)


Here are some links to articles that have helped me along the way:

- https://reactrouter.com/docs/en/v6/getting-started/concepts#matching
insert more links from repo here.