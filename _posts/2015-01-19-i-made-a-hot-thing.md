---
layout: post
title: I Made a HOT Thing
categories:
  - openstack-heat
  - orchestration
  - rackspace
---
Over the last few weeks I've busy working on a "out-of-the-box" sprint project. The result is an early release of [Foundry](https://github.com/rackerlabs/foundry), which is a more focused and workflow-oriented evolution of another of my side projects, [jsFormation](https://github.com/rdodev/jsFormation).

<!-- more -->

Why is it a "HOT" thing, you may ask? Well, for one, it makes a catchier title and secondly (and more importantly) is a web app to learn and build [HOT](http://docs.openstack.org/developer/heat/template_guide/hot_guide.html) based deployments.

### Philosophy
The overarching theme and philosophy of this app is one of lowering entry barriers and insuring, in as much as possible, positive outcomes.

#### Lowering Entry Barriers
Currently one of the main issues Rackspace Orchestration has is that in order to begin the user needs to install and setup an API client in their computer, then dive in the documentation or sample files that are hard to generalize. Unlike AWS's CloudFormation, as of this writing, Rackspace Orchestration doesn't offer a static list of resources it offers nor proper documentation for it. For a developer who has a strong reason to learn it, these obstacles might not seem all that steep; however, for someone who's merely curious, those same obstacles will likely be a bit too much and simply lose interest in the process. With Foundry there are _only_ two things a user needs:

  - A modern web browser
  - A Rackspace account with control panel access

that's it.

#### Positive Outcomes
One of the things that keep people interested in using/learning a new service is positive outcomes. That is to say, they follow the steps, they go through the process and at the end, the outcome is what they expect or they were told it would be. Foundry's approach to insuring positive outcomes is through an opinionated and constrained workflow. We deliberately pick and choose what aspects of building a template we expose the user to and we constrain the number of choices they have to make down to handful that are known to work and get the user to a positive outcome.

### Open Source From The Get Go
As with most aspects and tools we build at Rackspace, this web app is released† as open source and under the MIT license. Usage and details about contributing can be found in the Foundry repository linked above.

### Where To Next?
The first thing on our plate is adding 2-3 relevant resource types (services), likely Object Store, Block Storage and Networks, but nothing written in stone yet. 

### Feedback/Thoughts
I would like to hear your ideas for features or what use case can the app accommodate to make it even more useful. So, visit the [issues](https://github.com/rackerlabs/foundry/issues) section of the repo and chime in.

† I'm using "released" in its most literal sense (i.e. making it publicly available), not in the marketing or product cycle sense.