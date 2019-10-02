---
author: pavsaund
categories:
- DevDiary
date: "2014-10-26T16:56:31Z"
disqusIdentifier: "4836167967"
geo_public:
- "0"
guid: http://pavsaund.wordpress.com/?p=288
id: 288
tags:
- bdd
- bugs
- craftsmanship
- tdd
- testing
title: Acceptance driven bugfixing
url: /2014/10/26/acceptance-driven-bugfixing/
---

<em>I originally posted this on <a title="Acceptance driven bugfixing" href="http://blog.dolittle.com/2013/06/04/acceptance-driven-bugfixing/">the dolittle blog</a></em>.

There's a new task waiting for you in your inbox... a <strong>bug</strong> in production! Maybe the bug is completely unrelated to  code, you've created, but the report is there waiting for you. It's critical, and has to be fixed "today" or "ASAP"! And with a number of consequences, like "this feature is vital!", "support center is being called down by angry customers", "we're losing millions!".

<!--more-->

So given the levels of above chaos, you as a developer, have the power to put things right! Roll up your arms, it's firefighting time.
<ul>
	<li>Recreate the bug locally</li>
	<li>Find and fix the offending code</li>
	<li>Push and verify the code to production!</li>
	<li>Voila! You just saved the day! Woohoo!</li>
</ul>
But wait...there are more bug reports ticking in...seems like you just broke some other vital part of the application. Ah well, there goes that pay-raise.

We've all had this happen to us at one time or another. We produce software that meets all the given business requirements, software that adheres to SOLID principles but somehow happens to contain a bug.
<h3>How to avoid that mistake?</h3>
Bugs are inevitable, no matter how methodical you are as a developer, or how thorough the product owner is, there will be aspects you've overlooked, or an edge-case that no-one has considered.

Well-defined tests are one of the better ways to document how any given part of an application works, especially if written as specifications. When you look at it this way, a bug is a certain part of the system that hasn't been specified enough. The error could be bad user stories or bad implementation, but there's a certain aspect that someone has missed. Following test-driven / test-first principles, the obvious solution is to find a test that's missing some additional assertions, or introduce new tests that cover this aspect of the system. Either way, after this you should have red tests confirming the bug in the application. From this point in, it's just the red-green-refactor mantra, and you've fixed the bug, hopefully improved the code a little and, most importantly, added more documentation for the next dev that needs to look at this code. Now you can feel a lot more confident when pushing the fix to production.

This approach has worked extremely well for me. As with the test-driven process, I often don't know how to fix the buggy code, I just know that something in a given method is wrong, and I have a red test showing me what to fix. Giving yourself this harness also decreases the chances of adding "just another if" with unknown (long-term) consequences.

Now, imagine an entire team of devs working in bug-fix mode... how many new bugs are being introduced in the application if all you're focused on is "getting that fix out"?