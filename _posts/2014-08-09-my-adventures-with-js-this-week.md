---
layout: post
title:  "My Adventures With JavaScript This Week"
date:   2014-08-09 11:45
categories:
  - ES6
  - Map
  - mutable-keys
---
In spite of having programed JS for nearly two decades -- to varying degrees, of course: from fiddling with my Geocities home page to full-time front-end development --, it's one of those languages that tends to break away from the norm, usually not in the expected way. Which is why lately I've made a point to RTFM every time I bump into an issue or bug I suspect the language definition has something to do with it. 
 <!-- more -->

### The `delete` keyword
I've used `delete` sparingly throughout the years and, for the most part, it behaved as I'd expect, it removes/undefines the variable from the current scope or object. However, as I found out this week, it *only* works for deleting bound properties of an object. That is to say:

{% highlight javascript false %}
var such = "this";
delete such; //does nothing and returns false 
             //'such' is an unbound scope variable
many = "wow";
delete many; //deletes and returns true 
             //because 'many' is implicitly bound to the window object
var obj = {};
obj.such = "that";
delete obj; //does nothing and returns false
delete obj.such; //deletes 'such' property and returns true
{% endhighlight %}

### EcmaScript 6 `Map()` Objects
Late in the week I saw a tweet by [Addy Osmani](https://twitter.com/addyosmani) announcing the availability of ES6 `Map()` in the latest version of Chrome Canary. [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) seems like a pretty neat augmentation of plain ol' `{"java":"script"}` type of objects and with built-in setters, getters and queries, it can help in certain use cases. Neat, but not super remarkable. A bit later, Addy mentioned in a tweet that the keys for this map can be anything (gasssppp!) even mutable types. Now, let me preface this by stating that there's nothing inherently wrong when they keys of a hash map are mutable. Dangerous? Hazardous? Sure, but not inherently wrong. So, I replied to Addy bringing up the issue with mutable types as keys of the Map. After some push back from other twitter users, I set to find out how to prove why mutable types as keys is a bad practice. In the process I found out yet another 'crafty' (or clever) thing JS does.

##### The Quest For a Proof (Of Concept)
One of my first attempts at showing the hazards of having mutable types as keys was the following:

{% highlight javascript false %}
var such = {'c':1};
var obj = {such: "this"};
console.log(obj.such); // prints "this", OK
such.many = "wow"; // mutate key
console.log(obj.such); // prints "this", WTF!?!
{% endhighlight %}

After thinking over how JS was able to keep track of the key-value pair after I had mutated the key, the only logical thing seemed that it keeps track of the object's reference, not the value or its hash. Not completely content with that answer, however, I moved to my second attempt at showing the dangers of using mutable types as keys:

{% highlight javascript false %}
var such = {'c':1};
var obj = {};
obj[such] = "this";
console.log(obj[such]); // prints "this", OK
such.many = "wow"; // mutate key
console.log(obj[such]); // prints "this", OMG NOT OK!
{% endhighlight %}

"How's this black magic possible? Was everything I was told about mutable keys a lie? What kind of world do we live in?" At that point, I was feeling convinced (and somewhat defeated) that JS had a super awesome reference tracking mechanism and using mutable types as keys was 'OK' and safe, after all. But no, I'm too obstinate to give up that easily, so I moved on to my third attempt to settling this mystery once and for all:

{% highlight javascript false %}
var such = [1, 2];
var obj = {};
obj[such] = "this";
console.log(obj[such]); // prints "this", OK
such.push("wow"); // mutate key
console.log(obj[such]); // prints "undefined", BOOOOM!
{% endhighlight %}

Aha! The proof is in the pudding! I had figured out how to 'break' the magic. But then I was even more curious why it had worked with an array, but not an object. So, I went back and set up second example above again. Same result. Flummoxed, I decided to try my chances as shown below:

{% highlight javascript false %}
var such = {'c':1};
var obj = {};
obj[such] = "this";
console.log(obj[such]); // prints "this", OK
such.many = "wow"; // mutate key
console.log(obj[such]); // prints "this", OMG NOT OK!
console.log(obj[{}]); // prints "this", lolwut?
var moar = {"no": "way"};
console.log(obj[moar]); //prints "this", omg, seriously?
{% endhighlight %}

Alright! It seemed I figured that one mystery. Turns out JS was using the *type* `[Object object]` as the key, which is why mutating the key had no apparent effect. However, this is now beyond the Danger Zone™, this could (and probably has) thrown someone for a loop for hours or days wondering why their data is getting overwritten or messed up. Next up was trying to figure out the mystery of the first example above. So, I set it all up again, ran it and got same result. As I started tinkering with things in the Chrome console, I noticed the following:

{% highlight javascript false %}
var such = {'c':1};
var obj = {such: "this"};
console.log(obj.such); // prints "this", good.
console.log(obj[such]); // prints "undefined", o.O
{% endhighlight %}

After thinking a bit and given what I had learned, that last `console.log` printing undefined made a bit of sense. In that statement, I'm asking the object to retrieve the value whose key is `[Object object]` which there is none matching. I had a suspicion why this was the case, but had to prove it, so with the code above still in the console I typed the following: 

{% highlight javascript false %}
console.log(obj['such']); // prints "this", ;) check. mate.
{% endhighlight %}

So, that's the mystery of JS objects: they don't have any Eldritch or Lovecraftian enchantments to keep track of mutating keys. They do two things, depending how you set their properties:
1. if you set their properties inline or through dot notation (i.e.: `obj = {clap: "your hands"}` or `obj.clap = "your hands"`), JS will stringify the variable name and use it as the property key.
2. if you set the properties via `[]` notation, all bets are off how it will handle it. For many objects it will use that object's type, for arrays it appears it uses a string representation of the array and its elements. But it's inconsistent, so avoid using this form of populating objects (or Maps). 

### Closing Thoughts
Mutating keys are bad, mmk? While JS might be able to handle some of the cases, it's just a bad idea. Just because you can, doesn't mean you should, and this one is definitely a case when you shouldn't.

> NOTE: while the examples above were crafted using plain ol' JS objects, they have been tested with ES6 `Map()` and show the exact same behavior.
