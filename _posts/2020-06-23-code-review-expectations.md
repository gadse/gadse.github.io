---
title: "Code Reviews And Expectations"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - work
  - code review
---
I had an interesting conversation at work the other day. A colleague started it by asking for our expectations towards a code review. We do such reviews quite often and try to never roll out production code that hasn't been reviewed at least once. So, naturally, reviewing another developer's code is something we do often. However, we never spoke about a common set of expectations when it comes to reviews.

During the 30-minutes long and very fruitful discussion, two major positions emerged:
  - Reviews are there to improve the *code*.
  - Reviews are there to improve the *coder*.

The difference is small yet important. Obviously, given an infinite life span, improving the code*r* would be the one solution and we would have been done discussing after merely 3 minutes. However, reality is not so simple.

Now consider that the coder has a *finite* life span and therefore a finite time span during which the improved coder can write his automagically-improved code, and that giving and receiving a review both cost a significant amount of time and energy. Now add to that the fact that not everyone is able to learn from in-depth criticism at any given point in time. Personal struggles can occupy one's mind and impair communication between reviewer and author. The simple fact that it's right before lunch or time to go home can also have an impact on how well constructive criticism can be given and received. There are numerous reasons for why a review can fail to have a lasting and improving effect on a receiving developer.

So... what shall we do? On the one hand, we knew that the minimum outcome of a review is improved code.  Check ✔️. And we agreed that often enough it doesn't have to be the original merge/pull request's author that hast to perform the improvements.

But can't we do more? After all, we have an interest in our colleagues to become better developers. We haven't found an answer to this question yet, but we have agreed to discuss this topic again in about a week.

I think that having a look at [PEP20, the Zen of Python](https://www.python.org/dev/peps/pep-0020/), can be very enlightening in this moment - as it can be so often in life. Right there, in line 2, it says:
> Explicit is better than implicit.

Once again, when it comes to communication of any kind, PEP20 has an answer. It might not be _the_ answer, but being explicit in one's communication is rarely a mistake. So, for the time being, I answer the question of "what do I expect from a code review?" the following way:
> I expect functionally improved code. Except for when I ask for "more". Then I expect that on which the reviewer and I agree. And I'll be grateful whenever I get more than functional code improvements.

That's all for today. Stay safe and happy coding! 👋