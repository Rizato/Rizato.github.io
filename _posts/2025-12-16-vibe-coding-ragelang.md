---
layout: post
title: "Vibe Coding Ragelang!"
date: 2025-12-16
author: Rizato
tags: [update, langjam]
---

## Vibe Coding

Vibe coding is using a coding agent to write the code instead of doing it myself. 
It’s fast, handles languages I’m not experienced with, and can bypass the steep learning curve.

I didn’t think I could finish Ragelang on time solo, but vibe coding let me implement the entire language in a day. 
I’ve built a language as part of a team, [Rundown](https://github.com/mjkoo/rundown), for a Langjam, but that was four years ago, and I’ve likely forgotten most of it.
I completely skipped relearning how to build a language, AST, etc. 

I also skipped learning TypeScript. I’ve worked on existing TypeScript code bases, but creating a project from scratch was a different challenge. I wanted the game in TypeScript so it would run in the browser; requiring a download in past jams meant fewer people tried it.

I'm pretty happy with this choice, as I have four days left to work on the game itself.
That gives me more time to build fun features, create interesting art, and more.


## What did I ask it to build?

I prompted Cursor (with Opus 4.5), to implement the language I described in [yesterday's blog post](https://ragelang.com/blog/2025/12/15/introduction-to-ragelang/).

It built out the full runtime, parser, lexer, ast, canvas rendering, and the falling code preprocessor.
It all even worked!

After that it was just adding more and more features that I didn't think of for the blog post.
A good number of those things were already handled by the initial code generation.
It added all kinds of builtins covering trigonometry, some math, drawing shapes, etc.

In addition, I had it add music, sound, mouse/keyboard/touch handling, buffered inputs, and more.
It was fast enough that I even had it add a bunch of Python list/dict handling, prototype literals, and Rust-style enums.

It has definitely surpassed what I could have done by the end of the jam.

## VSCode Extension

One of my early goals was a simple vscode extension for the language.
While the experience is meant to be frustrating, I still want it to be possible.

I wanted error highlighting at a minimum to detect which characters were unsupported.
It recursively checks over the whole file, detecting characters above the immediately unsupported characters, that would become unsupported.

However, the LLM did it so fast, I added some more features.

* basic syntax highlighting with support for (almost) all the builtin functions
* ctrl-shift-v to show how everything will fall
* ctrl-shift-h to toggle error highlighting for falling characters

You can find the extension in the repository under `vscode-ragelang`.

## Did I learn anything?

That is the big drawback to anything AI.
I don't understand the code, and I have not learned to build a language.

Usually I do a game jam to learn something.
Just last week I did the Advent of Code, for that purpose; a challenge and a learning experience.

It's as weird mix of feelings, seeing my idea come to life so fast, but without my direct execution.
I'm basically the idea man that came up with the language, but not building it.
Using AI has taken the challenge away.
In previous models, I had to at least occasionally specify algorithms or data structures, but not anymore.

If the barrier to implementation keeps dropping, are we about to see the rise of the "idea person"?

## Writing code in Ragelang

I haven't experienced any rage thus far, but it is definitely annoying & tedious!

As a reminder, this language requires that all characters in the file be supported.
Any character without a supporting character (below, with wiggle room to the left or right), will fall.
It will fall until it lands on another character, or falls out of the file completely.

Once I had a basic implementation, I went ahead with some example games.
The AI built the bouncing ball, and platformer examples, but I manually added supports.

As an experiment, I did try having the AI do the supports, and it way over-supported everything.
It just basically filled all extra columns top to bottom with `// | | |...`.

 This could be improved with a supports algorithm, but as I stated yesterday, I don't want that!

So, I found myself doing all the supports.
With the extension, it is actually pretty easy.
The highlighting tells you exactly what is unsupported, so you can iteratively fill in all the supports.

I did some support optimization, trying to keep the code readable.
In a lot of cases, it didn't really do much, but I do like this little thing I found for the triangle supports. 

Just removing a few supports makes the triangles look much better. 
It's a minimal absolute difference, but a significant improvement in aesthetics. 

```
 | | | | | | | |  | | | | | | | |
  | | | | | | |    |   |   |   |
   | | | | | |      | | | | | |
    | | | | |        |   |   |  
     | | | |          | | | |
      | | |            |   | 
       | |              | |
        |                |
        |                |
```


## Playground

There is now a playground where you can mess with ragelang!
The documentation is definitely a work in progress.

Try your hand at building with ragelang on the [playground](https://ragelang.com/playground/)


## The Game

Starting tomorrow, I get to start building the game.
I still am not sure what I am going to be building, beyond being a 2d rage game.

I hope to take full advantage of all the existing features, and maybe even add a few more.
After the game is done, I will prune the language down and remove unused features. 
