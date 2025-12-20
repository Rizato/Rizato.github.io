---
layout: post
title: "Fledgling Progress"
date: 2025-12-19
author: Rizato
tags: [update, langjam, gamejam, fledgling]
---


I've been hard at work on Fledgling today.
I was getting too bogged down in art at first, but realized I need to make the game, and see what art I can get done in whatever time is left.

Starting from the AI generated template, I've built out the controls, camera, and a bit of obstacles.

With 25 hours left, I'm not sure I can get any art or sound effects done.
I was scrolling through asset stores, but didn't like any of it.
So, it may be color shapes if I can't finish. 
I do have a little chickadee I did up in pixel art, but that is it. 

I really want to have those dumb faux-deep voice lines when you reach random points or fall, so I hope to get some of that done. 

Who knew the game would be the hardest part of this project.


## Ragelang Supports

I mentioned in Discord and yesterday's blog post that I was going to try to make it more difficult to support the code.
I dedicated a bit of time today to trying to turn it into like a poly-bridge style game, but with static loads, as the code is static.
There was no way I was going to try something like adding extra load whenever a bit of code is being executed.
That would have been very cool, but even more work.

However, after working on Fledgling for many hours, the current supports are enough of a pain in the ass.
While autocomplete helps quite a bit, you still have to do a lot of editing.
When you make a bit of code longer, you can end up painstakingly adding dots to that line and every line below it.
Each line, just tapping `.` until it lines up.

I used to be lazy about letting extra `.` sit at the end of strings, because I figured it would just fall off.
Then some bit of code below got longer, and suddenly the `.` would drop into that statement.
Now I do a full guard across any long line, and surround it above and below with `.`s.

I think I hit the right balance, where I am getting annoyed with it, and it is making me more mad than playing the game. 

Mission accomplished!



