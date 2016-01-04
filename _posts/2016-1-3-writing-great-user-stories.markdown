---
layout: post
title:  "Writing great user stories"
description: "As a user story writer, I want to write great stories so that I can be clear to developers"
date:   2016-1-3 06:44:27 -0600
categories: user stories
---

>As a *user story writer*, I want to *write great stories* so that *I can be clear to developers*

One of the projects I have been working on lately has required me to write a large number of user stories for the other developers on the project. Part of the time has been spent essentially teaching our product owner to write stories independently, since we were having to work with him to get the stories broken down and clear enough for a developer to simply pick up and work with minimal previous knowledge required.

This is a great ideal for stories, but it's easier said than done. In this project I noticed some of my own assumptions making their way into some of the stories that I wrote, because of my knowledge of the problem domain. I had to rework my perspective when righting some of the stories to force myself to write the stories for other developers and not myself. Below are some of the techniques and concepts I use to reel in my perspective.

## User / Role clause

Use this to narrow the scope of the story and add a more refined perspective for the _who_ of the story.

* Reference a specific user role, preferably defined in the project documentation.
* Avoid simply declaring “as a user”. This is usually too broad.

## Goal / Desire clause

Use this to address the _what_ or the _goal_ of the story while avoiding referencing concrete functionality concerns (Acceptance Tests will cover those).

* Be specific about what a user must accomplish. If this part of the story isn't granular enough, it will not establish clear scope boundaries for a developer.


## Benefit clause

Use this to address the _why_ of the story. I feel that this clause is often hastily written, which is unfortunate, since many times a developer can come up with better alternative ideas about how to accomplish _what_ when given the _why_.

* Bring perspective to the business or user benefit. Sometimes the real benefit is not necessarily for the user themselves. It could be for customers or other external entities.

## Acceptance tests
Acceptance tests should address much of the specific interface requirements. If a user story defines the feature's scope boundary, the Acceptance tests are the fence posts in that boundary. When writing ATs be think about a story from a developer’s perspective. Understandably this degree of granularity can be difficult for someone who isn't a developer.

* Acceptance tests should have complete coverage of story boundaries.
* Ideally Acceptance tests should correspond to automated tests (unit, integration, UI).


## Overall concepts

### [ELI5] (https://www.reddit.com/r/explainlikeimfive/)
When possible try to write a story as if you were writing it for a five-year-old. Simplicity is key in user stories.

* Use basic words and avoid jargon.
* When domain-specific jargon is necessary create a term dictionary or wiki for new developers.

### Atomic stories
Each story should be as independent as possible.

* Granularity makes stories easier for developers to digest and work.
* Referencing multiple areas or components in an app can be a story smell. The story may need to be broken into multiple stories.

### Annoyances
Sometimes stories are unavoidably reliant on each other. Project management apps sometimes provide tools to account for this.

* Epics are course-grained user stories which can encompass many child user stories.
* Setting up blocker tasks can establish precedence of stories.
