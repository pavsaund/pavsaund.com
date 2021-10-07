---
layout: blog
draft: false
title: Building resilient frontend architecture
date: 2021-10-07T20:32:48.755Z
coverSize: partial
thumbnailImagePosition: ""
tags:
  - frontend
  - architecture
  - technical-debt
categories:
  - DevDiary
---
Notes on the talk on [Building Resilient Frontend Architecture](https://www.youtube.com/watch?v=TqfbAXCCVwE) by Monica Lent.

In this wonderful talk, Monica cuts to the heart of core aspects of rewriting code and presents 3 strategies to increase the resiliency of frontend architecture.

## Why do we usually rewrite code?

Inexperience, it's fun, better solution available and (the big one 🥁) **Technical debt 🎉.**

Monica's definition of Technical debt: 

> **Code that negatively and repeatedly affects the speed or quality of delivery.**

She continues to dig into technical debt, and the tendency to do big bang refactors to "fix" said debt, only to see them build up again. Or "Technical debt on a subscription model"🤣.

> The **real cost** of software is not the initial development but **maintenance over time**

## Constraints for a more resilient architecture

> Architecture as **enabling constraints** - Constraints about how we use data and code that help us move faster over time

1. “Source code dependencies must point inwards” => “Easier to isolate impact of changes”
2. "Be conservative about code reuse" => "Avoid coupling code that diverges over time"
3. "Enforce your boundaries" => "Preserve architecture over time"

## In conclusion

**💰The real cost of software is maintenance over time, because change is inevitable.**

**🚘Architecture is about applying enabling constraints to how we use code and data**

**🐿We can make small changes to make our projects more resilient**

* Think directionally
* Be conservative on reuse
* Enforce your boundaries

... and in addition - architecture from different languages and areas can be applied to our frontends. Be open to learning and adapting.