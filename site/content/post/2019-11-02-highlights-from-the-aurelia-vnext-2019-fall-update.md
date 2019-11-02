---
layout: blog
draft: false
title: Highlights from the Aurelia vNext 2019 fall update
date: 2019-11-02T20:37:42.809Z
coverSize: partial
thumbnailImagePosition: ''
tags:
  - aurelia
  - frontend
  - development
  - javascript
  - typescript
categories:
  - DevDiary
---
[There was a recent blog post with the status of Aurelia vNext](https://aurelia.io/blog/2019/10/31/aurelia-vnext-2019-fall-update/). For those of you that don't know, Aurelia is a frontend framework with a focus on standards, extensibility, ease of use and performance. It's been a while since a new major release, so vNext is a pretty big deal.

<!--more-->

These are some highlights of what I found pretty cool:

* Official name: **Aurelia 2**
* [VSCode integration](https://github.com/aurelia/vscode-extension/pull/104) with direct linking between bindables, observables, views, and custom attributes to their backing code representation
* VanillaJS-like performance with JIT (Just in time) optimisations, and a new AOT (Ahead of Time) optimisations 
* [Extensibility](https://aurelia.io/blog/2019/10/31/aurelia-vnext-2019-fall-update/#extensibility) that allows you to emulate the syntax of other frameworks, like Angular / Vue etc
* A continuous focus on [Web Standards](https://aurelia.io/blog/2019/10/31/aurelia-vnext-2019-fall-update/#web-standards)
* Developer Experience has recieved som pretty considerable features, here are the ones I'm excited about
  * More lifecycle hooks, and they are now synchronous. (no more queueMicroTask!)
  * New Router 🙌
  * Functional API's
* Multiple Integration scenarios that allow nesting of frameworks, and connecting other libraries directly in the underlying pipeline and more
* Extensive Test Tooling support, helpers and libraries.

The team is focused on keeping the migration path straight forward, through they have mentioned there'll be a few breaking changes. 

A lot of these improvements are raising the bar so high that we're bound to see more developers discover the joys of using Aurelia, as well as making that transition a lot easier for them with extensibility points.

I'm pretty excited about the future of Aurelia 2, but doubt I'll be getting my hands dirty just yet. Looking forward to a preview / release candidate before I start testing it out, and more of the WIP features are in place.
