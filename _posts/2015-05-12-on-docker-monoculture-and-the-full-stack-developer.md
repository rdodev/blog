---
layout: post
title: On Docker Monoculture And The Full-Stack Developer
categories:
    - culture
    - technology
    - developers
published: True
date: 2015-05-12 20:47:20

---

#### The Docker Monoculture

Unless you've been living in the woods away from all technology going through a Henry David Thoreau phase lately, you have surely heard of [Docker](https://www.docker.com/) a few hundred times already. 

<!-- more -->

Our industry has the tendency to obsessively and single-mindedly "rally" around certain technologies with no regard whether that technology makes sense for a given use case at all. In fact, as an industry, we reward that behavior. The hotter any technology is, the more you start seeing an "ecosystem" built around it, VC funding and even the so-called "enterprise" start funding projects that depend or build on that technology. We're currently seeing that with Docker. In all its promise and potential, Docker is becoming the alpha and omega of every aspect of software development: package management, developer environments, production deployments, and even crazier usage.

To be perfectly clear, this is _not_ a rant against Docker at all. It's a case against building a monoculture around it (or any other technology for that matter). Much like the proverbial fitting of the square peg in a round hole, we're seeing an increase in companies, developers and other to use Docker as both a crutch and panacea.

![](https://media.licdn.com/mpr/mpr/p/7/005/07a/078/3ffedef.jpg)

It reminds me of the heyday of Ruby on Rails in 2005-2006. Same behavior towards it, same insistence by managers to use it, so-called consultants pushing it to all their clients, same "if you aren't using Rails, you're probably a software dinosaur" attitude. 

We, as an industry, need to snap out if it. Docker is great at some things and nonsense for other things. Make sure the use case is a good fit. Don't treat it like it will fix all your technical debt or somehow make your application more efficient.

End rant.

#### The Full-Stack Developer

Unfortunately, there has been a bit of controversy about recruiters and hiring managers requiring/hiring full-stack developers. On the one hand, this "label" can be, and likely is, abused by aforementioned actors to mean "we want one sucker to build our entire application". 

But, on the other hand, from the hiring angle, I would like to hire a "complete" or generalist developer for certain positions. I would like the candidate to understand how all the tiers of the system work, at a fundamental level, even if they will be responsible for maintaining and engineering a small slice of said stack. I would want candidates to understand the potential performance repercussions on the back-end of their UI design, the API, the architecture, etc. I would want them to know how a database model change might bust the DB integrity or how some queries might trigger an outer join instead of a straight selection, how their application tier design can affect automation and so forth. In short, I would like to hire a *well-rounded developer* even if their focus is, as said above, a small slice of the stack.