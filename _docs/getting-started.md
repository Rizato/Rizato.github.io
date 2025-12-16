---
layout: doc
title: Getting Started
description: Learn how to install and start using Ragelang
order: 1
---

# Getting Started with Ragelang

Ragelang is a simple, approachable programming language designed for creating 2D games. It features a clean syntax, built-in game loop, and easy-to-use drawing functions.

## Quick Start

### Installation

Install Ragelang via npm:

```bash
npm install ragelang
```

### VS Code Extension

For the best development experience, install the Ragelang VS Code extension:

1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X / Cmd+Shift+X)
3. Search for "Ragelang"
4. Click Install

The extension provides syntax highlighting and the ability to run your games directly in VS Code.

## Your First Program

Create a file called `hello.rage`:

```rage
// My first Ragelang program

draw {
  clear("#1a1a2e")
  text("Hello, World!", 200, 200, 32, "#ffffff")
}
```

This simple program:
1. Clears the screen with a dark blue color
2. Displays "Hello, World!" in white text

## Understanding the Game Loop

Ragelang has two special blocks that form the game loop:

### The `draw` Block

The `draw` block is called every frame (~60 times per second) and is where you render graphics:

```rage
draw {
  // Clear the canvas
  clear("#000000")
  
  // Draw shapes
  circle(300, 200, 50, "#ff0000")
  
  // Draw text
  text("Score: 0", 10, 30, 16, "#ffffff")
}
```

### The `update` Block

The `update` block is also called every frame and receives `dt` (delta time) - the time in seconds since the last frame:

```rage
x = 100

update(dt) {
  // Move 100 pixels per second to the right
  x = x + 100 * dt
}

draw {
  clear("#000000")
  circle(x, 200, 20, "#00ff00")
}
```

**Important:** Always multiply speeds by `dt` to ensure frame-rate independent movement!

## Basic Drawing

Ragelang provides several built-in drawing functions:

```rage
draw {
  // Clear the canvas
  clear("#2d3436")
  
  // Draw a filled rectangle
  rect(100, 100, 50, 30, "#e74c3c")
  
  // Draw a filled circle
  circle(300, 150, 25, "#3498db")
  
  // Draw a line
  line(50, 250, 350, 250, "#2ecc71", 2)
  
  // Draw text
  text("Ragelang!", 200, 50, 24, "#ffffff")
}
```

## Variables and State

Variables are declared by simple assignment:

```rage
// Game state
player_x = 300
player_y = 200
score = 0

draw {
  clear("#000000")
  circle(player_x, player_y, 15, "#00ff00")
  text("Score: " + score, 10, 30, 16, "#ffffff")
}

update(dt) {
  // Move player to the right
  player_x = player_x + 50 * dt
  
  // Wrap around
  if (player_x > 600) {
    player_x = 0
    score = score + 1
  }
}
```

## Handling Input

Ragelang makes input handling easy:

```rage
player_x = 300
player_y = 200
speed = 200

update(dt) {
  // Arrow key / WASD movement
  if (held("left")) {
    player_x = player_x - speed * dt
  }
  if (held("right")) {
    player_x = player_x + speed * dt
  }
  if (held("up")) {
    player_y = player_y - speed * dt
  }
  if (held("down")) {
    player_y = player_y + speed * dt
  }
}

draw {
  clear("#1a1a2e")
  text("Use arrow keys or WASD to move", 10, 30, 16, "#dfe6e9")
  circle(player_x, player_y, 20, "#e74c3c")
}
```

### Input Functions

- `pressed(action)` - True on the frame an action starts
- `held(action)` - True while an action is held
- `released(action)` - True on the frame an action ends

Available actions: `"left"`, `"right"`, `"up"`, `"down"`, `"jump"`, `"action"`, `"a"`, `"b"`, `"start"`, `"select"`

## Creating Objects with Prototypes

Use `prototype()` to create objects with properties:

```rage
// Create a player object
player = prototype()
player.x = 100
player.y = 200
player.speed = 150
player.health = 100

// Or use object literal syntax
enemy = {x: 400, y: 200, speed: 50}

draw {
  clear("#000000")
  // Draw player
  circle(player.x, player.y, 15, "#00ff00")
  // Draw enemy
  circle(enemy.x, enemy.y, 15, "#ff0000")
}
```

## Defining Functions

Create reusable code with functions:

```rage
// Define a function
fun draw_player(x, y, color) {
  circle(x, y, 20, color)
  circle(x - 7, y - 5, 5, "#ffffff")  // Left eye
  circle(x + 7, y - 5, 5, "#ffffff")  // Right eye
}

// Use the function
draw {
  clear("#2d3436")
  draw_player(100, 100, "#e74c3c")
  draw_player(200, 150, "#3498db")
  draw_player(300, 100, "#2ecc71")
}
```

## Using Arrays

Arrays store collections of data:

```rage
// Create an array of enemies
enemies = []

// Add some enemies
i = 0
loop {
  if (i >= 5) {
    break
  }
  enemy = {x: 50 + i * 100, y: 100, alive: true}
  push(enemies, enemy)
  i = i + 1
}

draw {
  clear("#000000")
  
  // Draw all enemies
  i = 0
  loop {
    if (i >= len(enemies)) {
      break
    }
    e = enemies[i]
    if (e.alive) {
      circle(e.x, e.y, 15, "#ff0000")
    }
    i = i + 1
  }
}
```

## Control Flow

### If / Else

```rage
if (health <= 0) {
  game_over = true
} else if (health < 25) {
  status = "critical"
} else {
  status = "ok"
}
```

### Loop with Break

```rage
// Count from 0 to 9
i = 0
loop {
  if (i >= 10) {
    break
  }
  print(i)
  i = i + 1
}
```

## Example: Simple Bouncing Ball

Here's a complete example of a bouncing ball:

```rage
// Ball properties
ball_x = 300
ball_y = 200
vel_x = 150
vel_y = 100

draw {
  clear("#1a1a2e")
  circle(ball_x, ball_y, 20, "#e74c3c")
  text("Bouncing Ball", 10, 30, 20, "#ffffff")
}

update(dt) {
  // Update position
  ball_x = ball_x + vel_x * dt
  ball_y = ball_y + vel_y * dt
  
  // Bounce off walls
  if (ball_x > 580) {
    vel_x = -vel_x
    ball_x = 580
  }
  if (ball_x < 20) {
    vel_x = -vel_x
    ball_x = 20
  }
  if (ball_y > 380) {
    vel_y = -vel_y
    ball_y = 380
  }
  if (ball_y < 20) {
    vel_y = -vel_y
    ball_y = 20
  }
}
```

## Next Steps

Now that you have the basics, explore:

1. **[Language Reference](/docs/language-reference/)** - Complete documentation of all features
2. **[Examples](/docs/examples/)** - More complete game examples

Happy coding with Ragelang!
