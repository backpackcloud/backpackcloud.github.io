---
layout: podcast
title: I See Dead Problems
category: right-in-the-middle
number: 7
duration: "14:22"
description: Start with the solution... and you will have a big problem to solve.
tags:
- rum
- problem solving
- solutions
- prove you're wrong
- I still can't leave my glass filled for more than 1 episode
image: ritm-cover-small.jpg
audio:
  url: https://f000.backblazeb2.com/file/right-in-the-middle/Right+in+the+Middle+-+007+-+I+See+Dead+Problems.mp3
  size: 34730371
---

_Script_

Teca, I'm so tired today. It seems I've been fighting against all my nightmares at the same time. The output changes
even if I change the documentation. I think I need vacations.

...

Yeah, maybe just a nice sleep would do. You know, I've been into a lot of troubles ever since I started my career.

...

I guess the first freaking moment I can remember is a "try/catch" block being used as an "if/else" block. It worked, but
it looked so horrendous... at that time.... I was so ingenuous, that was a fluffy dog compared to what was waiting for
me. I even got the chance to write something worse.

...

I had to write an alert for when the disk utilization goes beyond... 100%. You can imagine how many times that alert was
fired.

But, you know, the most consistently crazy code I've seen was during one of my hard times working on a software where no
one was allowed to see the source code for the middleware we were coding. They created a buggy middleware in Java and
denied access to its source code. That was the reason why I had to learn bytecode. Surviving in that wild depended on
it.

We also had another constraint: no internet access... none... zero... nada!

...

That's a good point, Teca. I don't know why they block access to the code and the internet. It sounds like they don't
trust people. That is a common issue even these days. If you don't trust your people, why would you hire them? It
doesn't make sense to me. At least it didn't at that time.

...

I can't say it's true for all the cases, but I can't think of any scenario I was involved where the root cause wasn't a
company coding a solution instead of solving a problem. Software engineers were hired not to think about how to solve
the problem but to code something the company was sure it's gonna solve a problem... without even knowing if that was
indeed a problem to solve.

From there you can guess how things were going. No room for creativity because the solution was dictated. No need for
internet because you should just write the code, not think about solving something that is, in theory, already solved.
No room for testing because the solution is proved to work in 4 spreadsheets and 2 slide presentations, and it has to
hit the market asap, because, as soon as the market is aware of the solution, they will start suffering from the
problem.

...

Yes, Teca! No one was focusing on the problem, only in the solution. They were not prepared to be wrong, so they didn't
challenge themselves. In the end they had to persuade customers to buy the solution for a problem no one was having.

...

Well, Teca... there are some reasons why someone would buy a solution for a problem they don't have, but I want to keep
my sanity and not talk about that... Instead, let's talk about why it's important to focus on the problem.

Right now, my problem is: there is no rum in my glass. Come on, let's fix it.

===

Teca, of course you remember about our Science Driven Development. This is actually way more broad than it appears.
Proving you're wrong is actually the base foundation for everything we do. When companies start with a solution, they
look for the problem it solves, usually on a very biased approach, because starting with a solution doesn't allow room
for being wrong.

On the contrary, when companies start with a problem, they can challenge themselves, reframe the problem until it
becomes clear, understand what needs to be solved and not how it's gonna be solved. This is the perfect scenario for
proving you're wrong. In this case, real data is the key to prove you're wrong. Then the problem starts to show up.

...

Good question, Teca! The fact that the problem is discovered doesn't mean you're now gonna solve it. Some problems are
not worth to be solved, and the reason varies. Maybe it would cost too much to solve, maybe it's not aligned with the
company's strategy, maybe it's not even something the market would pay for having it solved. That is actually why I
don't believe in delivering more than what was agreed.

...

I know, I know... maybe I went too far...

Imagine you were assigned to solve a problem. You just finished the task but then you suddenly have a thought about
solving another problem that you are sure it's gonna be appreciated by the customers, and you do it. Congratulations!
You've just created a problem instead of solving one!

You basically assumed that you were right without collecting any real evidence that the new problem indeed exists. Even
worse, there are teams responsible for discovering and prioritizing the problems that the company will solve, so you
just bypassed them instead of working together with them. And it gets worse and worse. The extra work will need to be
maintained, who's gonna own this? Will this create a technical debt in the future? Are the customers really in need of
this? Are they willing to pay?

Almost everytime the extra work comes from an opinion. Opinions are usually irrelevant as they are a limited perspective
that doesn't represent the market. Unless you validate it with real data.

...

Good observation, Teca! It might be that, instead of an opinion, the extra work was originated from actual data. Still,
there are so many people that needs to be involved in order to not only map the problem but also make sure it is worth
to solve and, more important, when it will be addressed.

But, of course, I'm talking about a happy scenario, where the problems are well defined and prioritized. Defining a
problem to solve is not hard, but it has to be done right or you would end up having the wrong feeling about doing more
than what was asked for.

...

I actually remember when we were working on a web crawler. We were building it for just one customer. The plan was to
create a database from two sources of public data, so the customer could use it to run some analysis.

But the problems were not well defined, so one specific was to parse a webpage. This might look ok, until we had an
issue: data inconsistencies directly from the source.

Some pages had data inconsistencies, so the invalid data were propagated to our database. We then created a base
validation for it and logged the inconsistencies so the customer could manually check if there was an issue during the
extraction or a data inconsistency.

This sounds like we have delivered more value than what the problem was demanding, but that problem wasn't well defined.
It defined "how" we were gonna solve something, which means, it defined the solution, which was to parse a web page. So,
when we delivered the "extra validation feature", it sounded like we did more and it was actually appreciated. But, in
reality, we defined a solution and implemented another one that was more accurate then just parsing some HTML. If the
problem was well defined, our solution would be just a good solution to that problem. Since such situations are often
praised, it cultivates the "need to do more", which will cause waste of time (and money), if the problem is well
defined.

That's why I don't believe in delivering more than what was expected. We should write better problems instead and
deliver a solution for that problem.

So, how can we better define a problem?

...

Let me just solve my rum problem first...

===

Teca, what if I ask you to give me a bubble bowl?

...

Yeah, I'm sure you would just go out and buy a very nice bubble bowl for me. But what if I ask you to give me something
that enables me to enjoy the sea life in the comfort of this cabin?

...

Exactly! Now you have a lot of options. A bubble bowl would work, but also a fancy aquarium, or even a digital aquarium.
But hold on a second, we're on a ship, even a window would work! If I could see the plank, of course!

Now, what about something that would help me to get from a point A to a point B?

...

Correct, Teca! This is not enough information. If the point A is close to the point B, a bicycle would work. A car might
work as well, but this also depends on more information. If we're talking about Copenhagen, a bicycle is pretty much
your only choice. If we're talking about a small city in the countryside, an electric car might not work because of the
possible lack of charging stations. It's getting more clear that we always need a bit more information. What do you
think it is?

...

It's context! Without context, any potential solution cannot be verified. If A is Earth and B is Mars, an electric car
would only make sense if it's attached to a rocket.

Getting back to the bubble bowl example, if I ask you to give me a bubble bowl, I'm not asking you to solve my problem,
I'm just asking you to bring me the solution I came up myself. This gets worse because I'm not an expert in that field.
If I have a problem that I can't solve, I should hire someone qualified to solve the problem for me, not to deliver my
own solution. Remember, Teca: I have to prove that I am wrong. So, even if I think I have the solution, I need to be
challenged.

That's what should have happened with that web crawler project, we were not asked to solve a problem, we were asked to
implement a very specific solution. It doesn't matter if it's right or wrong. Build the thing right, not the right
thing.

That's not a way to solve problems, it's a way to cause problems. Way more effective than my chaos magnet, but not fun.

===

You know, Teca... after we started with our Science Driven Development approach, we noticed that it could be applied to
a bunch of different scenarios, so it became our Prove You're Wrong approach. Our projects now don't start without the
real problem to solve, we can't be limited by one particular solution.

...

You're right, Teca! Limitations breed creativity, indeed. But it's not all kind of limitation that will make our
creativity shine. Most importantly, defining the problem is the very first thing you need to do to actually solving it.
Failing to do so will introduce the bad culture of delivering more because the problem was actually an invalid or
incomplete solution.

Prove you're wrong instead, challenge your problem statement, reframe it until you get the best definition, and, only
then, use your creativity to find the best solution.