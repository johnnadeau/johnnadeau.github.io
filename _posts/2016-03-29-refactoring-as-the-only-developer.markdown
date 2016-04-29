---
layout: post
title: "Refactoring as the Only Developer"
date: 2016-03-29 19:29
published: true
tags: refactoring legacy code
comments: true
---

I recently gave a talk at the [Haverhill Hackers Meetup][meetup] about *"real refactoring"* where I
went through a few refactorings I had made in our codebase at [QueueDr][queuedr]. The examples were
dumbed down a bit for simplicity sake, but the motivations and changes made were clearly displayed.
The talk went well and I think those who attended(including myself!) learned a few tricks to bring
into their own codebases.

When you start a new project and you are the only developer working on it the possibilities seem
endless. No worrying about other hands getting into the codebase and messing everything up. No
dealing with shitty legacy code. Then a funny thing happens. *Your* hands get into the codebase and
mess everything up. *Your* code becomes the shitty legacy code you feared. You quickly realize that
you are capable of all the things you complain about, **and that completely fine.**

Business happens. We rush things, skip testing, and write horrible hacks(that we *intend* to fix
sooner and not later). Outside pressures have a direct effect on code quality. At the end of the day
though, having something working and shipped today is far better than something perfect
weeks/months/years from now. All code can end up being legacy code, even if you wrote it.

This is why refactoring has to be part of your process even if you are the only one touching the
code. It's unrealistic to think you'll write everything the way it *should* be the first time
around. So, put on  your refactoring hat and get going. Start small. There is no need to be afraid
and become paralyzed at the thought of embarking on this refactoring journey, no matter how horrible
the codebase has become. It'll be worth it. 

[queuedr]: http://queuedr.com
[meetup]: http://www.meetup.com/HaverhillHackers/
