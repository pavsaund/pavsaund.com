---
title: Does Aurelia Support React Hooks?
date: 2019-10-01T20:58:11.000Z
tags:
  - aureliajs
  - javascript
  - react
  - vue
  - frontend
---
There was recently a post on the Aurelia Discourse that caught my attention asking how react-like hooks would work when using Aureliajs. The [response from Aurelia's creator](https://discourse.aurelia.io/t/how-we-react-hooks/2955/2?u=pavsaund) underlined some of the reasons why I trust Aurelia to build JavaScript applications with Aurelia.

<!--more-->

Rob raised three aspects that Aurelia had that alleviated the need for "hooks"

> With Aurelia, we don’t need hooks because we have three very powerful things:
>
> * Observability
> * Dependency Injection
> * Metaprogramming

He continues in his post to describe how Aurelia doesn't try to re-invent the wheel but instead use time-tested OOP-practices that cater to Separation of Concerns.

**On Observability:**

> With Aurelia, we can observe normal objects/class properties. So, you can leverage the last 40ish years of OOP techniques and battle-tested approaches to building software. Also, the general observer pattern has been around for a very long time and has scaled to some of the most complex apps today.

The interesting aspect here is that he explains how the patterns of other frameworks (React / Vue) leverage different techniques, and tools to compensate for their lack of support for full observability. With Vue coming in close to Aurelia, with some edge-cases that are uncovered.

**On Dependency Injection:**

> On the other hand, Aurelia has a very powerful DI framework. This lets you decompose any problem into small pieces that work together to tackle something complex. Need to make something reusblabe? Just factor it out into a new class and inject it wherever you need. That’s a basic form of composition that works very well, with decades of history behind it.

**On Metaprogramming:**

> None of the frameworks have metaprogramming capabilities like Aurelia. In Aurelia’s case, you can apply a decorator to a class, and the framework will use your declaration to “write” code for you, so you don’t have to. We take this further with conventions. So, you can write vanilla js, following a simple pattern, and Aurelia will write code for you to make things into custom elements, etc...

**Some reflections**

Rob ends the piece by encouraging people to keep up to date on trends & techniques, but not to forget the years of learnings that have gone into existing techniques that work.

I also think it's important to recognize that there are different kinds of applications where features from React or Vue make more sense to use. Either because of the features those languages have, or because of the community support they have with plugins, libraries and helpers.

_<small>Originally posted on the [Dolittle Community Forum](https://community.dolittle.com/t/does-aurelia-support-react-hooks/33?u=pavneet)</small>_
