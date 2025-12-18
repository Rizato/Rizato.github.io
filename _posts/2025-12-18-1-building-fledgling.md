---
layout: post
title: "Building Fledgling"
date: 2025-12-18
author: Rizato
tags: [update, langjam, gamejam]
---

I missed yesterday's blog post, as I was in the middle of some changes at the end of the day.
So this is a midday update.

## Documentation

I went through all the generated examples and added supports and fixed the bugs.
I also added them to [playground](https://ragelang.com/playground/), so you can play with them without having to copy/paste.

## Fledgling

I've finally settled on a game idea.
Fledgling is a game about a baby bird that has fallen from its nest and wants to get back home.
The player starts on the ground and has to climb all the way back up to the nest at the top of the tree.

It has some basic controls: a/left-arrow for left, d/right-arrow for right, space to jump, and hold space to glide.
It's a bit of cute animal fun in a rage game with some Spyro inspiration.

## Building Fledgling

I initially wanted to build the game myself with no AI, but I gave up on that already.
I have to do a bunch of yard work to get ready for family coming in for Christmas, so having AI do the majority of the work lets me do both.
As self-punishment, I am still doing the supports manually.

### Results

Unfortunately, I hit the usage limit with Cursor Pro plan and Claude Opus 4.5, so I am stuck with their auto tier.
I do have a $50 extras limit, so when touching the language, I still use Claude.

After working with Auto to generate the initial Fledgling code, it was immediately apparent that it is not at the same level as Claude Opus 4.5.
It tried to build the game in JavaScript, which is doubly wrong, as I wanted it in Ragelang, and the repository itself was in TypeScript.
Then, after telling it to use Ragelang again, it tried to do supports despite being told not to, and just went infinitely wide with the supports getting hung.
The code it generated had many syntax errors: it was dropping curly braces, trying to use `not|or|and` instead of `!/||/&&`, making up random builtins, using existing ones wrong, and using properties available in javascript but not ragelang.
Issues with a new language are not surprising, given it has had no training with that language, but it required a lot of hand holding and back and forth chatting.

Claude, on the other hand, generated mostly correct unsupported code in the examples.
I did end up removing a few language features that I didn't like after I saw them in the examples, but that is the extent of my complaints.

Thankfully, I had properly supported the code, so fixing issues was pretty straightforward.
Any syntax errors had an accurate line number, so I was able to fix them quickly.

With respect to the game, it is way off.
AI is not capable of being creative, it just generates based on its training input.
When it comes to features, like movement, coyote time, and input buffering, it nailed it.
When it comes to level design, it is just bad. 
I am going to have to manually build the level, and all the obstacles.
Overall, I am still happy with it.
I think it still managed to code much faster than I could, and it produces runnable games.

I really need to just get to work on the art, level design, and sounds, which is honestly the most fun part of building a game anyway.

## Ragelang Language updates

Through working with examples and Fledgling, I made some improvements to the language.

### New Builtins

* `height()` - gets canvas height
* `width()` - get canvas width
* `frames()` - get number of frames so far
* `time()` - get time since the epoch in seconds
* `load_scene(path)` - load another ragelang script by path

### Fixes

* Fixed pattern matching allowing code blocks
* Added short-circuit boolean evaluation
* Removed .length property from arrays and strings

### Issues with supports

Filling in the supports on all the examples and Fledgling showed me something was wrong with my ragelang concept.
One of my thoughts with the supports is that you wouldn't want to do a giant box, because it would be unreadable and tedious.

I had been using `|` to represent a vertical support, but it is both visually large, and requires shift to type.
Instead, I started just holding `.` to fill in the columns easier.
As an added bonus `.` is much smaller, and easier for your brain to just filter out.
It looks like the whitespace marks I turn on in my editors anyway. 

On top of that, Cursor started offering autocomplete suggestions with `// ...` for every row I was on.
It didn't even have to be perfect, as extra `.` will just fall out of the page when processed.

I may have to make the ragelang comments more restricted to incentivise making patterns in the supports, or otherwise optimizing supports.
Something like a percentage limit of comment non-whitespace characters vs the non-comment, non-whitespace characters count.
My priority is currently Fledgling, but if I have extra time I will revisit.

### Thoughts on modules

When working on Fledgling I ran into another tough decision.
The code for Fledgling is definitely hard to read, as intended.
As more features are added and the level is built, it will become unmaintainable.
I considered adding modules and imports to break up the source, but ultimately decided against it for the same reason that I won't add auto-supports.

I did however make a compromise with `load_scene`.
It allows you to take completely independent parts of the game and separate them out into different files.
It completely resets the ragelang state and wipes out all variables.
I am using it for the start game screen, and the victory screen.

In the end, the game itself is still a tower of a file with all the code to make it run, and all the required supports, just without the extra code to run a simple menu animation.

## Next steps

For the rest of the jam I will continue to work on Fledgling.
I have a dev platform built, so I can experiment and build it out.
There is still a lot to do.
The gameplay currently is a barebones platformer that is very buggy.
I have to build out the full level, fix the controls, and also create a bunch of art.
I can do very basic pixel art, but this will be a challenge for me.

I still have two and a half days to get it done. 
