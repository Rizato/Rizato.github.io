---
layout: doc
title: Getting Started
description: Learn how to install and start using Ragelang
order: 1
---

# Getting Started with Ragelang

Ragelang is a programming language where unsupported characters fall. This guide will help you get started writing your first Ragelang programs.

## What is Ragelang?

Ragelang is a game development language with a unique constraint: every character in your code must be supported by characters beneath it. Unsupported characters will fall until they hit something or fall out of the program.

This constraint creates an interesting challenge - you need to build support structures (using characters like `.`) to keep your code from falling apart!

## Installation

### Using the Playground

The easiest way to try Ragelang is through the [online playground](/playground). No installation needed - just open it in your browser and start coding!

### Using npm

Ragelang is available as an npm package. Install it in your project:

```bash
npm install ragelang
```

Then import and use it in your JavaScript/TypeScript code:

```javascript
import { Ragelang } from 'ragelang';

const ragelang = new Ragelang({
  canvas: document.getElementById('game-canvas'),
  basePath: './assets'
});

ragelang.load('game.rage');
ragelang.run();
```

### Local Development

For local development from source, you'll need:

1. **Node.js** (v16 or higher)
2. **npm** (comes with Node.js)

Clone the repository and install dependencies:

```bash
git clone https://github.com/yourusername/ragelang.git
cd ragelang/ragelang
npm install
npm run build
```

## Your First Program

Let's create a simple "Hello, World!" program:

```rage
print("Hello, World!")
######################
```

**Important:** Notice the `#` characters at the bottom? That's the **foundation**. Everything above it must be supported, or it will fall!

## Adding Support

The code above will work, but if you add more code, you'll need to support it. Here's an example with support characters:

```rage
// Welcome to Ragelang!
print("Hello, World!")
// ...................
######################
```

The `.` characters provide support for the code above. Without them, the `print` statement would fall.

## VS Code Extension

For the best development experience, install the Ragelang VS Code extension:

1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X / Cmd+Shift+X)
3. Search for "Ragelang"
4. Install the extension

The extension provides:
- **Syntax highlighting** for Ragelang code
- **Falling character detection** - highlights unsupported characters
- **Falling preview** - see what your code will look like after processing

## Basic Program Structure

A Ragelang program typically has this structure:

```rage
// Variables
player_x = 100
player_y = 200

// Functions
fun move_player(dx, dy) {
 player_x = player_x + dx
 player_y = player_y + dy
}

// Draw block - called every frame
draw {
 clear("#000000")
 circle(player_x, player_y, 20, "#ff0000")
}

// Update block - called every frame with delta time
update(dt) {
 // Game logic here
}
// . . . . . . . . . . . . . . . . . . . . . . . . . . .
######################
```

## Key Concepts

### Foundation

The foundation is a line of `#` characters. Everything above it must be supported. The foundation itself never falls.

```rage
your_code_here()
######################
```

### Support Characters

Use characters like `.` to support code above. A character is supported if there's a non-space character:
- Directly below it
- One column to the left below
- One column to the right below

```rage
long_function_name()
// .................
####################
```

### Falling Behavior

- Characters fall **straight down** in their column
- They stop when they hit another character
- If they fall past the foundation, they're removed

## Next Steps

1. **Try the examples** - Check out the [examples page](/docs/examples) for sample programs
2. **Read the language reference** - Learn about all the features in the [Language Reference](/docs/language-reference)
3. **Understand supports** - Learn tips and tricks in the [Support Structure guide](/docs/support-structure)
4. **Build something** - Start creating your own games!

## Tips for Beginners

1. **Always use a foundation** - Without `#` characters, everything falls out
2. **Start simple** - Begin with short programs to understand the support system
3. **Use the VS Code extension** - It will help you catch unsupported characters before running
4. **Guard long lines** - Protect your longest lines with supports above
5. **Test frequently** - Run your code often to catch falling characters early

## Getting Help

- Check the [Language Reference](/docs/language-reference) for syntax and built-in functions
- Read the [Support Structure guide](/docs/support-structure) for tips on managing supports
- Look at [examples](/docs/examples) to see how others structure their code
- Visit the [GitHub repository](https://github.com/yourusername/ragelang) for issues and discussions

Happy coding! Remember: keep your code supported, or it will fall! 🎮
