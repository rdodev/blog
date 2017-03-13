---
layout: post
title: A Brief Monologue About Date Input Fields
categories:
 - ux
 - ui
 - patterns
published: True
date: 2015-10-17 12:33:44
---

Of the many UI/UX anti-patterns you see out there in the world today, not very many come close to the level of frustration caused by date fields in forms. This frustration has two facets for me: as the end-user and as UX person.

<!-- more -->

#### Dropdown Misuse

Dropdown menus can be used very effectively when you want to restrict the number of choices shown to the user and retain control of the values entered in a given field. As a rule of thumb, a dropdown menu should not have more than 5-7 items in it. Further, the user should be able to see all the options in the dropdown list in one click, while it not covering other UI controls or needing the user to scroll. Unfortunately, dropdown are often treated as cop-outs for lacking a more coherent work-flow and user-minded experience. They are often used as a "cheap" way to avoid having to add an extra page to select relevant data or using a more complex control like a so-called combo box or make intelligent guesses of reasonable choice list.

##### (mis)Usage With Dates

I'm of the opinion that dropdown menus should not, under any circumstance be used for date fields. This usage is by far the worst offender among all dropdown menu misuses. I have come across, in several occasions, date fields consisting of three contiguous dropdown menus: one for the month (sometimes in number, sometimes by name), a dropdown for the day (1-31 regardless of month chosen, silly I know) and finally a dropdown for the year (which usually have 100+ entries). So, from the user perspective this presents a few challenges:
 
 * Selecting a day from a list of 31 numbers can and is error prone
 * Selecting a year from a list of 75+ is outright unreasonable

From the technical perspective it doesn't make much sense either. That date at some point in time, before posting to a service, will have to be parsed or put together into a standard date format for interoperability with other systems and services. So why have three different controls in the screen to take care of that not only makes UX terrible but also makes for hard work from the technical side? Rhetorical, I know. The answer is simple: don't use dropdown menus for dates. Got it? Good. Let's move on.


#### Field Masking

Field masking is the use of an free-form input guide for in-place replacement by the user. At some point in time, field masking was considered, by some, to be a decent way to deal with input constraints. However, this invariably resulted in opening the proverbial can of worms, technically speaking. Browser compatibility, event triggering order, input validation, etc. Even after many of the technical challenges were addressed, it still felt a bit hacky. And in many cases this turned into an egregious user experience.

##### Date Format Masking

Although I have not seen this anti-pattern in the wild as of last few years -- which is a good thing -- it's worth mentioning why it didn't work well for date fields. If you have a mask like `__/__/____` the user still has to guess which one is for month and which one is for day-of-month given both have two digit placeholders. Further, you would need to have a lot input validation after each keystroke since there's no way to guarantee the user won't enter nonsensical numbers `17/37/0000` for instance. And in addition to that, you would need to have some sort of aid to tell the user they were on/off track. Not only was this massively technically kludgy, but it made the whole thing fail even the most liberal of accessibility tests, miserably so. Main take-away, just say no to input field masking in general, but emphatically no for date fields.

#### Recommended Alternatives

So, up to now I've been telling you what to avoid and why you should avoid it. But what about some suggestions as to should be used? I'm going to address couple of them those below.

##### Date Pickers

Date pickers are not anti-pattern per se. The issue is they are only useful for a narrow range of use cases. For instance, while they can be effective to pick a date +/- 3-6 months, it suffers from navigation issues if it's a date way in the past or way out in the future. If your intended use case matches the criteria and narrow date range, you should definitely use a date picker for your date fields.

##### Input Hints

If you need to provide a free-form input for a date that can be a long time from the present (i.e. date of birth, date of retirement, etc.), you can provide input hints. Input hints are plain text indications, usually small font, that are placed very close to the input field and show the desired format (i.e. `YYYY-MM-DD`, `123-45-6789`, etc.)


#### Final Remarks

If there's just one concept I'd like a reader to take away from this blog post is to use dropdown boxes very, very judiciously, sparingly and deliberately, in general, and **avoid them entirely** for date input entry.