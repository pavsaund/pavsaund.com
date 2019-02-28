---
author: pavsaund
categories:
- Development
date: "2014-10-26T18:00:21Z"
dsq_thread_id:
- "4560849326"
geo_public:
- "0"
guid: http://pavsaund.wordpress.com/?p=287
id: 287
tags:
- boy scout
- business value
- craftsmanship
- tdd
- technical debt
- testing
title: The boy scout rule
url: /2014/10/26/the-boy-scout-rule/
---

Recently I had the discussion with a colleague on how new code was being added to a code-base without maintainability in mind. The discussion was sparked by a code-review that had been ping-ponging between the reviewer and the developer where readability and ( as a result ) maintainability was an issue.<!--more-->

The code review caught it this time, but this isn't always the case. It boils down to mindset when approaching a given problem to begin with, especially when <a title="Acceptance driven bugfixing" href="http://pavsaund.wordpress.com/2014/10/26/acceptance-driven-bugfixing/">bug-fixing</a>. Get in, fix the issue and get out with as little impact as possible. This is the so-called "fire-fighting mode" (other terms have been used, i.e. "task force" or "marine mode") and is fundamentally the opposite of the "boy scout rule". The boy scout rule's best companion is the rule of "opportunistic refactoring".

Here are some of my thoughts on the matter

<strong><a title="The boycott rule" href="http://programmer.97things.oreilly.com/wiki/index.php/The_Boy_Scout_Rule" target="_blank">Boy scout rule</a>:</strong>
<blockquote>...Always check a module in cleaner than when you checked it out.... - Robert C. Martin</blockquote>
<a title="Opportunistic refactoring" href="http://martinfowler.com/bliki/OpportunisticRefactoring.html" target="_blank">Opportunistic refactoring</a>:
<blockquote>...any time someone sees some code that isn't as clear as it should be, they should take the opportunity to fix it right there and then - or at least within a few minutes... - Martin Fowler</blockquote>
Cruft and technical debt build up over time or new requirements change the premise for what the code is attempting to solve. So when writing code many developers struggle with these rules, because they do not believe they are actually adding value. I think they believe that it's often easier to just fix functionality in the quickest way possible rather than taking a step back to assess what the feature actually is attempting to solve. Many <del>arguments</del> excuses are used to justify not adhering these rules:
<h3>"But if it works, there's no need to spend more time to improve the code".</h3>
The code is in production, it has been tested by users and it works as desired. If you don't need to change it, then I agree that refactoring just for the sake of refactoring might not be the best thing to spend time on. If you need to change or extend it though, what then? My basic thought is this: If you are afraid of changing it due to possible ripple effects, then that's definitely reason enough to do more with it while you're there already. You should NEVER be afraid of changing the code.
<h3>"Not my code, not my responsibility"</h3>
Too many have this attitude. The code-base is going to be developed and maintained by different people and it's your responsibility to make it a good place to work in, day after day. In a way, it's too bad we can see who committed what in the VCS (Version Control System). It leads to a blame-game and personal ownership (blame) of features. Maintaining the code-base is every team members responsibility.
<h3>"This wasn't part of the estimates"</h3>
Estimation, agile and how we actually do are tasks are funny things that vary on a project by project basis. There are different understandings and requirements which play into the magic estimation number. The honest fact of the matter is that we usually know the most about a task the closer we are to actually starting on it. So if you estimated last week, and you've discovered something that drastically complicates the task, are your estimates still valid? Same goes with code and its complexity. This is something that arises when you are half way into solving an issue and you realise the need for a refactoring. It's something you have to deal with and there is no time like the present. You're already in there...fix it!
<h3>"We'll create a technical task for this"</h3>
This could be the natural outcome of the previous point. When we discover code-wtfs that increase the planned scope there is a tendency to separate this into a separate task or story. This implies that we can deliver functionality in the "existing" way first, then if time allows do refactoring. What happens is by being "agile" the developer implements functionality, and doesn't prioritise the refactor. Once the functionality task is marked as done and is tested, the "need" to refactor fades away. So at least we've marked the need to refactor in the backlog some place, right?

The right way to go about things is to do the needed refactoring as part of delivering functionality. There is no need for a separate technical task. You are doing what is required to deliver the needed functionality.

There will be times when the needed refactoring has large ramifications, and will actually have to be done as a separate task. This is something that has to be coordinated with the rest of the team, and at that point it is a group decision on the outcome.
<h3>"I can deliver more features faster, so that means I'm delivering business value!"</h3>
Business value is measured by many things. In the agile mindset there is an illusion that delivering business value means churning through the backlog as fast as possible without thought for the long-term maintainability. Though you may have high velocity in the beginning of a project, this will stagnate when change requests start ticking in. Which means a short delivery cycle, but a prolonged stabilisation / maintenance period. We have to write software that embraces change. Requirements always change after the user has started using the software.

Delivering business value also means delivering a maintainable solution.

Another approach is the spike and stabilise method, where you intentionally spike out code and allow changing requirements to form and adjust the end product. This also implies that the code you write will be overwritten and also maintainability will increase over time. This is usually a very conscious <strong>business decision. </strong>Not a developer-decision.
<h3>Wrapping things up</h3>
It's not always as black and white as I've described above, but the points are valid nonetheless. I believe we as developers have a professional obligation to deliver business value through well-crafted code that captures the business requirements and allows for modifications to be made when change is required.

At the end of the day it comes down to our values as developers and how we want to define ourselves.