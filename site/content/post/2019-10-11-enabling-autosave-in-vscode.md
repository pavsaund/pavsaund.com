---
title: "Should I enable Auto Save in VSCode?"
date: 2019-10-11T08:51:57+02:00
draft: false
categories:
- DevDiary
tags:
- vscode
- auto-save
- feedback-loops
- growth
- tools
- workflow
- productivity
keywords:
- tech
summary: I've decided to experiment with the auto save feature on, but first I wanted to dissect WHY I'm so skeptical of it, and what I could potentially gain. Here's a brain dump.

#thumbnailImage: //example.com/image.jpg
---

I worked on another developer's machine yesterday and they were using the auto-save feature in their editor. This threw me off completely, and had me questioning a fundamental truth I've had of needing to save files while developing software. 😱

{{< tweet 1182543783327649792 >}}

I've decided to experiment with the auto save feature on, but first I wanted to dissect WHY I'm so skeptical, and what I could potentially gain. 

Here's a brain-dump.

<!--more-->

## Why am I skeptical of auto save while coding? 🤨
### More Load

* I tend to have automation running in the background (ie: build watchers for javascript and dotnet, as well as continuous testing tools)
* What are the consequences of triggering the watchers with every change?
* Memory / cpu battery life?

### Less Flexibility

  * I tend to leave things in a mess when refactoring sometimes, and I wonder if that will lead to more noise vs signal?
  * more distracted by things failing
  * I want to be explicit about when I'm ready to "commit" a change to disk with the save-feature.
  * I tend to have WIP as unsaved files as a very convenient feature
  * Sometimes I do changes before committing the previous ones - it's good then to be able to go bac, commit the saved changes, then save the new changes (more control)

### Personal Resistance 
* Old habits die hard
* Introducing a new source of friction (by removing friction) 🤷🏾‍♂️

## What I could potentially gain:

* I instinctively press CMD + S WAY too often during a work day
* Saving keystrokes is a bonus
* Knowing I'm always working on the latest bits while developing
* It's how I expect document editors to work by default (but they tend to commit on every save as well, leaving a changelog to navigate)
* Avoid Errors while working where a file isn't saved - Oh, the number of times this has happened
* Remove an entire layer of doubt and cognitive load from my day-to-day workflow
  * Am I really working on the latest bits? 
* Encourage smaller changes because it saves and triggers build / errors at faster
* Remove edge-cases when I typo and press CMD + Q/W (Quit, Close Window)

## To be Continued

Am I over-analyzing this? Perhaps. But it's because I had this strong reaction I want to understand, experiment, and learn.

So, I'm now turning on auto save in VSCode. Let's see how this goes.