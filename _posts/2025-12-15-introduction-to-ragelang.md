---
layout: post
title: "Introducing Ragelang!"
date: 2025-12-15
author: Rizato
tags: [announcement, langjam]
---

Welcome to the Ragelang blog. Hre I will be discussing the progress, decisions, and methodologies while building a language and game for [Langjam Gamejam 2025](https://langjamgamejam.com).



## What is Ragelang

ragelang is all about giving the developer the rage inducing experience of playing a rage game while developing.

In ragelang, all of a program's characters must be supported by characters beneath, or they will fall.
Falling characters will continue until they land on another character, or until they fall out of the program entirely.

Each ragelang program is made up of three parts; the found, supports, and the code itself.

### Foundation

The foundation is one or more `#` characters on a line that mark the base for all supports. 
The foundation can only exist once in a file, but can be as many or as few `#` on the chosen line. They can be spread out, or stacked up together. 
These characters do not fall.
Any code below the foundation will fall out.


### Supports

Supports are the structure that hold up the code. 
These can be made up of comments, or the code itself. 
To support a character, there needs to be a supported character below it, with some wiggle allowing for the character to also be the left, or right by one character.
This allows developers to make tree like supports. 

Here is an over-supported example.

```
print("Hello, World!")
// | | | | | | | | | |
//  | | | |   | | | |
//   | | |     | | |
//    | |       | |
//     |         |
//     |         |
//     |         |
//     |         |
//     |         | 
//     #         # 
```


### Code

The code that makes up ranglang is going to be a dead simple DSL focused on making 2D platformers.\
I haven't really fleshed all this out yet, I am definitely just making it up as I go here.
It will be changed in the future for sure.

*None of these snippets have supports, for simplicity.*

Each program needs to respond to a few events from the runtime that executes the game loop.

```
draw {} 
update(dt) {} 
```

The language will expose builtin functions that can be used to draw the game to the screen.

```
text(text, x, y, color)
sprite(path, x, y, color, outline)
```

There will also be a bunch of platformer specific helper builtins for things like coyote time, and jump buffering.

Additionally, it provides a `prototype()` that allows for custom fields and data in a container.

```
player = prototype()
player.health = 10
player.on_ground = true
player.jump_velocity = 9


```
You can use simple variables. 

```
gravity = 4.95 // in tiles per second per second
```

Plus a bit of control flow with if else blocks.


## Falling Characters May produce valid code

When a character falls, if it lands within the code, it may still produce a valid ragelang program. 
This may produce hard to identify bugs when the code is otherwise right, or may be used to intentionally to obfuscate the real intent of the software. 

Let's look at the hello, world example on the home page. 

```
//         to RageLang!
// Welcome  | | | | |
// | | | |   | | | |
// Author:    Rizato
print("Hello, World! ")
// | | | | |         |
######################
```

This software has an unsupported `World!`. 
This will fall, carrying everything above down as well. 
However, the output may be very different than you expect.
Falling characters fall until they hit another character, not until they hit a position that would have been supported.
Let's take a look at the final output. 

```
//
// Welcome  
// | | | |  o RageLa  
// Author: t| |||||| g! 
print("Hello, Rizaton")
// | | | | | |World!||
######################
```

You can see some initially supported characters fell all the way to the foundation.
You probably expected it to look a bit more like the following.

```
//
// Welcome to RageLang!
// | | | |  | | | | |
// Author:   | | | |
print("Hello, Rizato ")
// | | | | |  World! |
######################
```

The difference in behavior of supports vs falling characters is the major footgun in ragelang. 

Honestly, even I forgot how it works when writing the example, and had to edit my home page while writing this post.

## Could the supports be generated?

Absolutely, but I won't be building any tooling for that. 
The whole experience with ragelang is the frustration of trying to support everything, and trying to read/write code that is supported.

If a computer generates the supports, it is just clutter.

## Implementation

ranglang is intended to be an interpreted DSL.
The AST, parser, runtime, etc. will all be written in typescript for maximum web compatibility.

## Goals


I was unable to start on the 14th, so I will be running from the 15th forward.

My plan is still very loose, but here are my overall goals. 

1. Write ranglang implementation in typescript
2. Write a vscode plugin for identifying characters that will fall (but not generate supports)
3. Write a rage game, title TBD.
4. Build a website for playing the game, that includes a playpen for editing the game and running it


## Use of AI

I am using Cursor to help me write the code for this project. 
I plan to use the Opus 4.5 model with the cursor agent.


The game itself will be written by hand.
I want to feel the ~~joy~~ rage of writing a game in ragelang. 
There is no way I would bypass it. 


## Stay Tuned

I plan to do little daily blog posts, so you can follow along as I build.

Visit the [GitHub repository](https://github.com/Rizato/ragelang) to see the code.
