---
layout: post
title: "Rewrite code from scratch?"
date: 2013-10-24 11:18
comments: true
categories: 
---

As a developer, almost everyone has made a difficult choice, rewrite something from scratch. Joel Spolsky wrote [this](http://www.joelonsoftware.com/articles/fog0000000069.html) to explain why you shouldn't do it. There're some good reasons.

# Artical summary

The very important, but hidden reason,

> It's hard to read code than to write it.

It's definitly true. But no need to blame developers or the one made the rewrite decision. It's a nature fact in software. You don't necessarily have gone with the last version process, no memory, just code, may have spec or not, may have the code owner or not.

Then you may have bias to make the decision.

<!-- more -->

The old code is valuable because they are used, tested, bug found and fixed. The oppsite, if you throw them away,

- throw away knowledge
- market leadership
- put yourself in danger, you may have no shippable code for sometime

The old code can be used because,

- Architecture problems can be refactored, though it's not easy but you can still get it done.
- Performance issue can be solved by re-writing part of the code, not the whole.
- Ugly code is not a real issue.

# More thoughts

This ariticle is good because it clearly pointed out the bias on legacy code. Though it keeps saying "no need to rewrite", after indivisual understanded the bias, he can make the right desicion himself.

Some thoughts on the oppsite side,

- The technics, tools, methedologies are developing fast comparing to old times. Writing from scratch costs less than before.

- The cost of delievering slow is becomming bigger.

- The team morale of maintaining a legacy code should be considered

There should always be a certain threshold of choosing to rewrite. Avoid bias from each side, choose your own.
