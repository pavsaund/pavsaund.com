---
author: pavsaund
categories:
- Development
date: "2016-01-28T22:42:52Z"
disqusIdentifier: "4560843844"
guid: https://pavsaund.wordpress.com/?p=779
id: 779
image: /wp-content/uploads/2016/01/code-close.jpg
coverImage: /wp-content/uploads/2016/01/code-close.jpg
coverSize: "partial"
publicize_twitter_user:
- pavsaund
tags:
- mobprogramming
- agile
- business value
- code review
- conflicts
- pair-programming
- team
- trust
title: Long live Code Reviews! Code Reviews are dead!
url: /2016/01/28/long-live-code-reviews-code-reviews-are-dead/
---

<em>Let me introduce you to Skybert (pronounced Sheeburt, for those of that haven't grown up in Norway). He's my imaginary developer-friend currently working at Mega Enterprise Inc Ltd Corp. He's been butting heads with the lead developer, Jack,  for a while now. They don't seem to be seeing eye to eye on a feature that Skybert implemented. You see, Jack doesn't like how Skybert writes his code. Formatting is wrong and he uses way too long variable names, and he doesn't write a single comment and...(list goes on)! Jack hates reviewing Skyberts code. Skybert usually gets his code back from Jack, with a long list of TODOs. So Skybert goes off to re-do most of his work just to give it back to Jack...When Jack's finally happy with the code; It adheres to his preferred coding style and uses the correct enterprise patterns that have been decided upon. He allows it through the magic gates to master.</em><!--more-->

Now some of you may be in taken aback when reading this. Surely this isn't something that <strong>really</strong> happens? Well, as with any unbelievable story, it's <a href="http://myview.rahulnivi.net/code-review-important/" target="_blank">based on real life</a>.

Review feedback can be done in many ways. The traditional "<em>here's what I think is wrong</em>" or "<em>Hey, sit down with me and let's look at this together</em>" or "<em>I've found a few things here I'd like you to address, could we implement and assess this together?</em>" or "<em>A combination of the above, but then the reviewer implements his changes and asks the developer to do a review back</em>". That last way has some advantages for the reviewer. He provides value back as actual code. The original developer may not be available so instead of the story rotting in "on-hold" the reviewer can move it forward and maybe some else can review it.

Sometimes code reviews can be personal due to to tension between the developer and reviewer. Sometimes it's embarassing because of being shamed in front of the entire team in a group review. Sometimes it's disruptive because you can't get your work done when review-feedback interrupts your work on the next story. As long as there is a <a href="https://blog.nelhage.com/2010/06/i-hate-code-review/" target="_blank">shroud of negativity</a> around code reviews, they are going to be painful. Just a glorified manual gated check-in.
<h2>You're going about this all wrong</h2>
Well guess what? Code reviews <strong>are</strong> a manual gated check-in, but they <strong>can</strong> have great value. Consider a different approach. You're on a team delivering small, focused user stories that have a certain amount of value to your users. The team slices and pulls in the smallest amount of stories to deliver real value. Approximiately 1-2 weeks of work. The team's goal is to look at these stories and decide how to deliver this value to users. A part of the teams mantra is to have maintainable, quality code, and code review is the decided way to enforce this. The story continues...

<em>So Skybert has changed employers and is working at Super Agile Startup Gang. He's done implementing a feature and moves his story to the next column on their workboard. He announces to the team that there's a story for review. Since delivering value is the most important thing for the team, another team member,  Jenny, puts her task on hold to review Skyberts story. Alas. It doesn't look good. Since Skybert is new, there are several aspects of the existing system he hasn't taken into consideration. At this point of time <em>Jenny</em> hasn't actually looked at the code. She's been testing the functionality in the system. So <em>Jenny</em> calls Skybert over and asks if he wants to look at this together. They move the story back to "in progress" and start to dig into it. They get to the cause of the issue, and then<em> <em>Jenny</em></em> looks over some of the code with Skybert. They decide to continue on the story together. As they look at the code,<em> <em>Jenny</em></em> realises that Skyberts code doesn't match the teams formatting guidelines, so she points him to their linting tool that gives formatting warnings that are easy to correct. After this they take turns in implementing the desired functionality. When they're done Skybert has learned a lot about the teams approach to writing code and the existing system, but more importantly<em> <em>Jenny</em></em> has made a connection with him based on mutual respect and trust. The story can now be merged into master and work its way to the users in the next deployment.</em>

What is the difference in these two stories? No, it's not the agility / size of <em>Mega Enterprise Inc Ltd Corp</em> vs<em> Super Agile Startup Gang</em>, though there sometimes may be some correlations here. No, it's not the automatic linting to ensure formatting, though that helps in regards to familiarity in the code-base. No, it's not the fact that<em> </em>Jenny showed Skybert about the system, though  learning about the problem domain is essential. These are all side-effects of the <strong>real</strong> benefit here.

<strong>It's about the teams goal of delivering complete stories to their users through quality code that gives them value.</strong> Instead of thinking about her own task, Jenny prioritized completing the story on the way to production. They want the best possible experience for users so quality software written by a team that cares is what they are striving for. Because the focus is on the users, the team is aligned around this and can have a dialog about the code in an honest and respectful manner that doesn't pull in personal issues. This is also why Jenny decided to pair-program the review-feedback with Skybert.
<h2>So pair-programming review feedback is the take-away here?</h2>
Well, sometimes, it depends on the story, time-constraints and other priorities. But for many teams this would be a huge increase in team happiness and code quality. The take-away is doing what is right for the user with a team that is aligned!

So code reviews should be looked upon as an opportunity for learning for the developer and the reviewer. It's a safe place that is concerned only about the quality aspects of the code that has been written and the value it provides.
<h2>Wait...there's more.</h2>
What is the actual reasoning behind code reviews though? Why do we do them? They are usually put in place to ensure that new code added to the codebase isn't making it worse, and possibly also making it better. The idea is to have a second pair of eyes to remove potential bugs the developer has missed. The problem though, is that it's often too late to look at code in a review and make major changes to it since it may have been solved differently. Why do I say this? Because the reviewer can easily get as caught up in the way a feature has already been implemented (tunnel-vision) and not be open to alternatives.

The cheapest code to change is often that which hasn't been written at all. As developers we believe that the writing of code is our job. We get lost in this obsession to write more code even when we focusing on delivering value to our users.

https://twitter.com/GundersenMarius/status/681455350730633221

https://twitter.com/GundersenMarius/status/681456714441441280

The more you ponder on a problem up-front the easier it may be to find a good solution, with or without code. So, to avoid getting into the situation where the code reviewer is held hostage to the developers implementation, consider alternatives:

<strong>Pair-program</strong> the feature. This will give you a valuable second opinion to help guide yourself along the way and hopefully increase the chance of approaching the problem correctly. There are issues with this though. Even a pair can get blinded by a desired implementation especially when they are unmatched in skill, experience or understanding of the problem domain.

<strong>Mob-programming</strong>. With a team of developers looking at a single task at a time there is a lot more knowledge-sharing going on than at any other time. The team is communicating and building trust. There is a feeling of really building software together. And there is no need for reviews. The team is already there, they decide! I want to explore this space a lot more.
<h2>Finally</h2>
Code reviews can be painful, but with the right atitude and trust within the team, they can be extremely useful. With the right team and approach they can also be removed completely. Or used deliberately only when needed.

Now, I know I've spun this post off from being focused on the art of the code review to being about team dynamics. But I find these to go hand-in-hand.

I'm interested to hear what your experiences are with code reviews and what you do in your teams?

Please leave a comment or reach out to me on <a href="http://www.twitter.com/pavsaund" target="_blank">twitter</a>.

<i>Cover image used under CC from <a href="https://www.flickr.com/photos/ruiwen/3260095534">ruiwen.</a></i>