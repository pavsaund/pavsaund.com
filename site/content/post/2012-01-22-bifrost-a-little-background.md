---
author: pavsaund
categories:
- Development
date: "2012-01-22T01:22:55Z"
format: standard
guid: https://pavsaund.wordpress.com/?p=166
id: 166
tags:
- bifrost
- cqrs
- javascript
- knockoutjs
title: Bifrost &#8211; A little background
twitter_cards_summary_img_size:
- ""
url: /2012/01/22/bifrost-a-little-background/
---

In this past year at work, we’ve been in the process of developing a new platform from the bottom up with new functionality. One of the goals was to move away from an old unmaintainable solution to a new maintainable solution based on expected coding standards, and of course to meet the business' needs about scalability and rapid feature development. With an overloaded domain, responsibilities were mingling with each other and business rules and validation was all over the place. Based on our needs, we felt it was that CQRS was the way to go. <a href="http://en.wikipedia.org/wiki/CQRS">CQRS </a>has been the talk in the <a href="http://en.wikipedia.org/wiki/Domain_driven_design">DDD </a>community for a while, and this pattern was something we could really relate to. In comes <a href="https://github.com/dolittlestudios/bifrost">Bifrost</a>!

Originally a helper-project for <a href="http://www.ingebrigtsen.info/">Einar Ingebrigtsen</a>, we decided to leverage and contribute to Bifrost as an open sourced platform for web-app development. At it's very heart Bifrost adheres to CQRS and is taking it "to the next level" by delivering a platform to deliver rich web applications.

[caption id="" align="aligncenter" width="312" caption="Basic archtecture with an MVC application frontend - from Bifrost docs"]<a title="CQRS Overview, based on a MVC application" href="http://www.ingebrigtsen.info/Bifrost/documentation/Overview.html"><img src="http://www.ingebrigtsen.info/Bifrost/documentation/Figures/CQRS_Overview.png" alt="" width="312" height="379" /></a>[/caption]

Because of the way Bifrost as a platform was conceived, it has evolved in parallel with the product we are building. As project needs arise, amendments are made in Bifrost. This enables steady, controlled development on Bifrost without introducing features (too far) ahead of time. Though this is a good way of driving the project forward, it isn't building out all the aspects of Bifrost. On the plus side, the platform is well-tested, thought through, and works well (with some known limitations and needed improvements).

On the web aspect of things Bifrost supports ASP.NET MVC and works well with the framework. Validation and binding of commands is something that just works, and I'm sure it's something that people will appreciate. The next natural step is to actually not depend on MVC, and build out the client-side aspect of the platform. For this <a href="http://knockoutjs.com">Knockoutjs </a>comes in handy.

Knockoutjs is a JavaScript library that adheres to the <a title="MVVM" href="http://en.wikipedia.org/wiki/Model_View_ViewModel">MVVM </a>pattern, which can be traced back to WPF and Silverlight. This allows the view (html) and viewModel (data, behaviour, commands) to be separate, sharable pieces of code. What this gives us is a clear way to bind our Query data from the server to a UI, and allow commands to be fired back into the system.

Bifrost has its implementation of CQRS quite well done already, and with it  you can go in and whip up a great app with what's there now, but you're going to get little, to no help in regards to client-side features. There's a clear focus on developing for the client-side aspect of things as well, which will enable Bifrost as an application platform. It's a great convention-based platform that can solve many business needs, and its future looks bright :)

I hope to write more about the different aspects of Bifrost in the coming weeks. Until then, here's some further reading:
<ul>
	<li><a href="http://www.ingebrigtsen.info/">Einar Ingebrigtsens blog</a></li>
	<li>Bifrost:  <a href="https://github.com/dolittlestudios/bifrost">https://github.com/dolittlestudios/bifrost</a></li>
	<li><a href="http://codebetter.com/gregyoung/2010/02/16/cqrs-task-based-uis-event-sourcing-agh/">CQRS, Task Based UIs, Event Sourcing agh!</a> - Greg Young</li>
	<li>DDD: <a href="http://domaindrivendesign.org/">http://domaindrivendesign.org/</a></li>
</ul>