---
layout: post 
title: 'UX In The Command Line, part I'
categories:
  - ux
  - cli
published: True
date: 2015-10-18 11:04:54
---

This is a blog post that I've been meaning to write for at least a year (likely longer than that), but for any number of reasons I never got around to sit down and actually write it. This is the first of a few posts in this particular subject that it's so important and relevant to _ALL_ developers, yet often neglected in practice: command line interface user experience. In this installment, I will deal mostly with the hand-wavy aspects of the subject, while following installments will consist mostly of practical and technical content.

<!-- more -->

#### The Command Line

Today we tend to see the command line like a power tool for power users who can't be bothered or slowed down with a UI, or a way to execute binaries "closer" to the OS/metal or a way to "hide" features from the average user or also commonly, as of late, a way to run arbitrary commands during provisioning/automation. However, it's worth noting that not all that long ago, the command line was the only means of using and interacting with a computer from home users to research labs. While UIs are great and have helped the massive adoption of computers everywhere, the command line should be not be treated like a second-class citizen, given for granted or dismiss the need to think about UX.

#### Usability Issues

In my opinion, most of the issues command line tools suffer from derive from assumptions made about the user, misjudging utility and scope creep.

##### Assumption About The User

As briefly mentioned above, many command line tools make assumptions about the user. Some tools assume the user is familiar with the command line and other similar tools. Others assume the user knows standard flags and usage patterns. Other tools assume the user has access to online help and documentation and finally some tools just assume the user has psionic super powers and can read the mind(s) of the author(s).

##### Misjudging Utility

Although much less common than other issues that plague command line tools, this one is actually a bit accidental, if you will. The issue arises by someone writing a one-off command-line tool to automate a small task or to take the brunt of grunt work. Then said author releases it to the wild (maybe open source), then people with similar needs start finding the tool (presumably through a search engine) and then these users getting frustrated because they can't figure out the tool, doesn't have proper documentation and so forth.

##### Scope Creep

Scope creep is the bane of _any_ product development -- period. It affects all aspects of a product's UX and the command line is no exception. Maybe a command line tool was originally designed to cover X use cases by the time it ships, with increased scope, it covers X, Y and Z use cases. With the new scope and use cases poorly documented, arbitrary flags put in place, new required positional arguments and maybe even breaking backward compatibility.


----

As mentioned in the introduction, I will explain in more detail, provide examples as well as suggest how to fix and avoid each of the issues I mentioned in this blog post. Thanks for reading and I hope you'll keep an eye out for the next installments.