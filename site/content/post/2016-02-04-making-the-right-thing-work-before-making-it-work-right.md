---
author: pavsaund
categories:
- Development
date: "2016-02-04T00:29:09Z"
dsq_thread_id:
- "4559184586"
guid: https://pavsaund.wordpress.com/?p=1286
id: 1286
image: /wp-content/uploads/2016/02/plane.jpg
publicize_twitter_user:
- pavsaund
tags:
- architecture
- bdd
- code quality
- feedback
- spike &amp; stabilize
- tdd
- users
title: Making the right thing work before making it work right
url: /2016/02/04/making-the-right-thing-work-before-making-it-work-right/
---

I've been a SOLID<sup><a href="#reference-1">1</a></sup> fan of TDD over many years and have spent a lot of time drilling myself in writing tests first to drive applications forward. I truly believe I have been at a place where my <a href="http://blog.8thlight.com/uncle-bob/2012/01/11/Flipping-the-Bit.html" target="_blank">BIT has been FLIPPED</a>. There are occasions though when attempting to write tests first have just been hard and completing a feature with test-first has been a record in will power and what felt like an eternity to deliver a feature. But if it was easy then everyone would be doing it.

<!--more-->One of the strengths of TDD is when attacking a well-defined core problem. Either it's a specific change to a system that is test-driven down from the front-end, or a brand new feature. The intent is clear and the design naturally evolves.

But what about times when there is uncertainty around the solution? Maybe there's a new 3rd party integration lurking around? It's at these times going in head-first with test-driven guns ablazing I've felt most scorn. I wish I knew what I did now when I started.
<blockquote>You often know the most about a feature after you're done with it.</blockquote>
We should aim to reduce uncertainty. Remove the unknowns. It's time to put down the tools and mindset of TDD and enter the startup mindset.
<h2>Embracing uncertainty</h2>
There are <a href="http://blog.8thlight.com/uncle-bob/2013/03/05/TheStartUpTrap.html" target="_blank">pitfalls here</a>, but as developers we need to be able to use many different tools and approaches.

When there's a lot of uncertainty and the potential for high <a href="http://dannorth.net/the-art-of-misdirection/" target="_blank">opportunity cost</a> we must write the smallest amount of code possible to verify our assumptions.
<h3>Create, Rinse, Repeat</h3>
One of the best approaches I have used is the doing a <strong>Proof of Concept</strong>, or <strong>Create, Rinse, Repeat</strong> as I like to call it.

The idea is to brute-force your way to a solution to verify your most uncertain assumption. The main goal of this approach is to get that much desired feedback as soon as possible.

When you have that feedback, it's time to throw-away that code. Once you've got the needed answer you delete / reset and then redo it, properly. If there are other large uncertainties to be dealt with, then deal with these the same way.

Beware! I've seen a proof of concept shoe-horned in as the basis for new code far too often, which is why I like to use the term <strong>Create, Rinse, Repeat</strong>. Then there's no doubt about what should happen with the original code.
<h3>Spike &amp; Stabilize</h3>
There's another term I <a href="/2012/06/09/ndc-2012-impressions/" target="_blank">stumbled over</a> in a <a href="https://vimeo.com/43536417" target="_blank">talk by Dan North</a>. The idea here is to have moved "<a href="http://lizkeogh.com/2012/06/24/beyond-test-driven-development/" target="_blank">Beyond TDD</a>". You're at a state where abstractions, seperation of concerns, SOLID principles are almost second-nature to you. In many ways you are doing the same as hacking it out, but you're also identifying abstractions and making the code easy to change.

Now there are no guarantees that you are actually hitting the correct abstractions, but the point is, you don't know that until it's been put to use.

Once feedback starts ticking in and the truth of a domain starts to surface, then stabilzing the code with tests and making subsequent changes with tests make more sense.

This also ends up with a rewrite, but does so gradually over time. It requires discipline and very skilled individuals working as a team to pull it off without incurring tons of technical cruft.
<h2>The grey area</h2>
In a black &amp; white world it's easy to see which use-cases call for which approach. In everyday life when delivering software in a team this may not be so obvioius.

It's often when taking feature requests at face value, seeing the simple solution through the system and assuming you know the solution that redious re-writes have to be done. This is also where so many blame practices as TDD or BDD or pair-programming or anything that isn't just <a href="http://programming-motherfucker.com" target="_blank">programming motherf****r</a>.
<h2>Question assumptions!</h2>
<blockquote>Assumptions make an <strong>ASS</strong> out of <strong>U</strong> and <strong>ME!</strong>
<p style="text-align:right;"><em><a href="http://www.ingebrigtsen.info" target="_blank">Einar Ingebrigtsen</a></em></p>
</blockquote>
As I continue down my path of crafstmanship I have started to realise how important the human aspect of speaking to stakeholders / business owners and users is to creating usable software. These assumptions can have ripple-effects across your code-base and cause <a href="http://www.docondev.com/search/label/Technical%20Debt" target="_blank">technical debt and also cruft</a>.

We also need to wield the tools we have the right way, there is no silver bullet. I firmly believe that testing first is the cheapest way to provide maintainable software over time. Some people have this in their fingers without this mindset. I think these are the few compared to the many who disregard the value it brings.

Does this make sense to you? Have you had similar or opposite experiences? Please share your thoughts in the comments or contact me directly.

In the meanwhile: <strong>Question your assumptions and make the right things right!</strong>
<sup id="reference-1">1</sup>: Pun intended!

<em>Cover image used under CC from <a href="https://www.flickr.com/photos/deanhochman/20769348728">DeanHochman</a></em>