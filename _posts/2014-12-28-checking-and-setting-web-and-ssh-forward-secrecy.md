---
layout: post
title:  "Checking for and Setting Up Forward Secrecy"
date:   2014-12-28 20:45
categories:
  - security
  - NSA
  - ssh
  - tls
---

I would like to preface this post by making it abundantly clear that I'm neither a InfoSec expert nor a "hacker" of any sort. If anything, I'm not particularly well versed on this subject, so I'm posting this for both my own edification and sharing the knowledge.

<!-- more -->

Recently it has been [revealed](https://twitter.com/jonathanmayer/status/549333357033967616/photo/1) that the NSA might be using passive methods for intercepting, undermining and ultimately decrypting secure communications, specifically protocols or tools that do not use forward secrecy.

When I asked how to test for this "vulnerability" and how to fix it, [Paul McMillan](https://twitter.com/PaulM) provided the following *non-comprehensive* instructions and suggestions (which I will paraphrase given the benefit of not being constrained to 140 characters):

 - For your web servers, connect to them with a browser, using SSL, and look at the chosen key exchange suite. In Chrome, click on the green https lock or green highlighted organization name if it's an extended validation certificate. See image below for more details 

![SSL CERTIFICATE KEY EXCHANGE MECH](/assets/images/2014-12-28-forward-secrecy/ssl-cert-screenshot.png)

 - Check for `DHE-RSA, DHE-DSS` or `ECDHE-RSA, ECDHE-ECDSA` key exchange mechanism (see highlight in image above). If you can see that, you should be OK. If you don't see any of those, you need to change your web server's config as suggested [here](https://cipherli.st).
 - If you deal with clients on top of Windows XP, you need to remove support and suggest they upgrade their OS as well as using a modern, up-to-date browser (there are also many other benefits, so there are plenty of good reasons to encourage or even force this issue).
 - If you happen to be using Java as the backend, you *must* upgrade to Java 7.
 - For ssh, configure your server to only allow protocol version 2 and make sure your keys are reasonably strong, regenerate them if you aren't sure. This [site](http://blog.patshead.com/2013/09/generating-new-more-secure-ssh-keys.html) seems like a good place to start.
 
 While the suggestions above might seem like trivial, they actually make a big difference and are a big deterrent to extra-legal eavesdropping by US intelligence agencies as well as other unsavory groups that prowl the web looking for easy targets. So there really is no reason not to take a few minutes to make sure your servers' key exchange mechanism is up to snuff and how to fix that if it's not.