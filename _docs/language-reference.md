---
layout: doc
title: Language Reference
description: Complete reference for Ragelang syntax and features
order: 2
---

# Language Reference

This document provides a complete reference for the Ragelang programming language, including all built-in functions, control flow structures, and language features.

## Note

Not human reviewed for accuracy

## Table of Contents

- [Basic Syntax](#basic-syntax)
- [Data Types](#data-types)
- [Variables](#variables)
- [Operators](#operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Enums and Pattern Matching](#enums-and-pattern-matching)
- [Built-in Functions](#built-in-functions)

---

## Basic Syntax

### Comments

Use `//` for single-line comments:

```rage
// This is a comment
x = 10  // Inline comment
```

### Program Structure

A Ragelang program typically consists of:
- Variable declarations
- Function definitions
- A `draw` block (for rendering)
- An `update` block (for game logic)

```rage
// Variables
player_x = 100
player_y = 200

// Functions
fun move_player(dx, dy) {
  player_x = player_x + dx
  player_y = player_y + dy
}

// Draw block - called every frame for rendering
draw {
  clear("#000000")
  circle(player_x, player_y, 20, "#ff0000")
}

// Update block - called every frame with delta time
update(dt) {
  // Game logic here
}
```

---

## Data Types

Ragelang supports the following data types:

### Numbers

Both integers and floating-point numbers:

```rage
x = 42
pi = 3.14159
negative = -10
```

### Strings

Text enclosed in double quotes:

```rage
name = "Player"
message = "Hello, World!"
```

### Booleans

```rage
is_jumping = true
game_over = false
```

### Arrays

Ordered collections of values:

```rage
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", true]
empty = []
```

### Prototypes (Objects)

Key-value containers for structured data:

```rage
player = prototype()
player.x = 100
player.y = 200
player.health = 100

// Object literal syntax
enemy = {x: 50, y: 100, speed: 5}
```

### Null

The absence of a value:

```rage
result = null
```

---

## Variables

Variables are declared by assignment. No `let` or `var` keyword is needed:

```rage
x = 10
name = "Player"
is_active = true
```

Variables can be reassigned:

```rage
score = 0
score = score + 10

// Or use compound assignment
score += 10

// Or increment/decrement
score++
```

---

## Operators

### Arithmetic Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `+` | Addition (or string concatenation) | `5 + 3` → `8` |
| `-` | Subtraction | `5 - 3` → `2` |
| `*` | Multiplication | `5 * 3` → `15` |
| `/` | Division | `10 / 4` → `2.5` |
| `%` | Modulo (remainder) | `10 % 3` → `1` |
| `**` | Exponentiation | `2 ** 3` → `8` |

### Comparison Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `==` | Equal to | `x == 5` |
| `!=` | Not equal to | `x != 5` |
| `<` | Less than | `x < 5` |
| `<=` | Less than or equal | `x <= 5` |
| `>` | Greater than | `x > 5` |
| `>=` | Greater than or equal | `x >= 5` |

### Logical Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `and` / `&&` | Logical AND | `x > 0 and x < 10` |
| `or` / `||` | Logical OR | `x < 0 or x > 10` |
| `!` | Logical NOT | `!is_jumping` |

### Bitwise Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `&` | Bitwise AND | `5 & 3` → `1` |
| `\|` | Bitwise OR | `5 \| 3` → `7` |
| `^` | Bitwise XOR | `5 ^ 3` → `6` |
| `~` | Bitwise NOT | `~5` → `-6` |
| `<<` | Left shift | `1 << 3` → `8` |
| `>>` | Right shift | `8 >> 2` → `2` |

### Unary Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `-` | Negation | `-x` |
| `!` | Logical NOT | `!true` → `false` |
| `~` | Bitwise NOT | `~0` → `-1` |

### Compound Assignment Operators

Compound assignment operators combine an operation with assignment:

| Operator | Description | Equivalent To |
|----------|-------------|---------------|
| `+=` | Add and assign | `x = x + y` |
| `-=` | Subtract and assign | `x = x - y` |
| `*=` | Multiply and assign | `x = x * y` |
| `/=` | Divide and assign | `x = x / y` |
| `%=` | Modulo and assign | `x = x % y` |
| `&=` | Bitwise AND and assign | `x = x & y` |
| `\|=` | Bitwise OR and assign | `x = x \| y` |
| `^=` | Bitwise XOR and assign | `x = x ^ y` |

```rage
score = 0
score += 10    // score is now 10
score *= 2     // score is now 20

health = 100
health -= 25   // health is now 75

// Works with strings too
message = "Hello"
message += " World"  // message is now "Hello World"

// Works with object properties
player.x += speed * dt
player.health -= damage

// Works with array elements
inventory[0] += 1
```

### Increment and Decrement Operators

Increment and decrement operators add or subtract 1 from a variable:

| Operator | Description | Example |
|----------|-------------|---------|
| `++` | Increment by 1 | `x++` or `++x` |
| `--` | Decrement by 1 | `x--` or `--x` |

**Prefix vs Postfix:**
- **Prefix** (`++x`): Increments first, then returns the new value
- **Postfix** (`x++`): Returns the current value, then increments

```rage
x = 5

// Postfix: returns old value, then increments
y = x++    // y is 5, x is now 6

// Prefix: increments first, then returns new value
z = ++x    // x is now 7, z is 7

// Common use in loops
i = 0
loop {
  if (i >= 10) {
    break
  }
  print(i)
  i++  // Same as i = i + 1
}

// Works with object properties
player.score++
enemy.health--

// Works with array elements
counts[index]++
```

---

## Control Flow

### If / Else

Conditional execution with `if`, `else if`, and `else`:

```rage
if (score > 100) {
  text("High score!", 10, 10, 16, "#00ff00")
} else if (score > 50) {
  text("Good job!", 10, 10, 16, "#ffff00")
} else {
  text("Keep trying!", 10, 10, 16, "#ff0000")
}
```

Conditions must be enclosed in parentheses, and blocks must use curly braces.

### Loop

The `loop` keyword creates an infinite loop. Use `break` to exit:

```rage
i = 0
loop {
  if (i >= 10) {
    break
  }
  print(i)
  i = i + 1
}
```

#### Common Loop Patterns

**While-style loop:**
```rage
count = 0
loop {
  if (count >= 5) {
    break
  }
  // Do something
  count++
}
```

**For-each style (iterating over array):**
```rage
items = ["apple", "banana", "cherry"]
i = 0
loop {
  if (i >= len(items)) {
    break
  }
  print(items[i])
  i++
}
```

**Processing until condition:**
```rage
loop {
  // Process something
  if (done_condition) {
    break
  }
}
```

---

## Functions

### Defining Functions

Use the `fun` keyword:

```rage
fun greet(name) {
  print("Hello, " + name)
}

fun add(a, b) {
  return a + b
}

fun create_enemy(x, y) {
  enemy = prototype()
  enemy.x = x
  enemy.y = y
  enemy.health = 100
  return enemy
}
```

### Calling Functions

```rage
greet("Player")
result = add(5, 3)
enemy = create_enemy(100, 200)
```

### Keyword Arguments

Functions can be called with named (keyword) arguments:

```rage
// Positional arguments
sprite("player.png", 100, 200, 32, 32)

// Using keyword arguments for clarity
sprite("player.png", 100, 200, width=64, height=64)

// Keyword arguments can skip optional parameters
text("Score: 100", 10, 10, color="#00ff00")
```

---

## Enums and Pattern Matching

### Defining Enums

Enums define a type with distinct variants:

```rage
// Simple enum (unit variants)
enum Direction {
  Up,
  Down,
  Left,
  Right
}

// Enum with data (data variants)
enum PlayerState {
  Idle,
  Running(speed),
  Jumping(height, velocity),
  Attacking(damage, cooldown)
}
```

### Creating Enum Values

```rage
// Unit variants are used directly
dir = Up

// Data variants are called like functions
state = Running(5.0)
attack = Attacking(10, 0.5)
```

### Pattern Matching with `match`

The `match` expression lets you handle different enum variants:

```rage
enum PlayerState {
  Idle,
  Running(speed),
  Jumping(height)
}

state = Running(5.0)

// Match returns a value
description = match state {
  Idle => "Standing still",
  Running(s) => "Moving at speed " + s,
  Jumping(h) => "In the air at height " + h,
  _ => "Unknown state"
}
```

### Pattern Types

**Wildcard pattern (`_`):** Matches anything
```rage
result = match value {
  1 => "one",
  2 => "two",
  _ => "other"  // Catches all other cases
}
```

**Literal patterns:** Match exact values
```rage
match count {
  0 => "none",
  1 => "one",
  _ => "many"
}
```

**Identifier patterns:** Bind the value to a name
```rage
match some_value {
  x => x * 2  // x is bound to the value
}
```

**Variant patterns:** Match and extract enum data
```rage
match state {
  Idle => "idle",
  Running(speed) => "running at " + speed,
  Jumping(h, v) => "jumping"
}
```

---

## Built-in Functions

### Drawing Functions

#### `clear(color)`
Clears the canvas with the specified color.

```rage
clear("#000000")      // Black background
clear("#2d3436")      // Dark gray
clear("rgb(30, 30, 50)")
```

#### `rect(x, y, width, height, color, alpha)`
Draws a filled rectangle.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `x` | number | required | X position |
| `y` | number | required | Y position |
| `width` | number | required | Width |
| `height` | number | required | Height |
| `color` | string | required | Fill color |
| `alpha` | number | 1 | Transparency (0-1) |

```rage
rect(100, 100, 50, 30, "#ff0000")
rect(100, 100, 50, 30, "#ff0000", 0.5)  // 50% transparent
```

#### `circle(x, y, radius, color, alpha)`
Draws a filled circle.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `x` | number | required | Center X |
| `y` | number | required | Center Y |
| `radius` | number | required | Radius |
| `color` | string | required | Fill color |
| `alpha` | number | 1 | Transparency (0-1) |

```rage
circle(300, 200, 25, "#00ff00")
```

#### `line(x1, y1, x2, y2, color, width, alpha)`
Draws a line between two points.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `x1` | number | required | Start X |
| `y1` | number | required | Start Y |
| `x2` | number | required | End X |
| `y2` | number | required | End Y |
| `color` | string | required | Line color |
| `width` | number | 1 | Line width |
| `alpha` | number | 1 | Transparency (0-1) |

```rage
line(0, 0, 100, 100, "#ffffff", 2)
```

#### `text(text, x, y, size, color, alpha)`
Draws text on the canvas.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `text` | string | required | Text to display |
| `x` | number | required | X position |
| `y` | number | required | Y position |
| `size` | number | 16 | Font size |
| `color` | string | "#ffffff" | Text color |
| `alpha` | number | 1 | Transparency (0-1) |

```rage
text("Score: 100", 10, 30, 24, "#ffffff")
text("Game Over", 200, 200, 48, "#ff0000")
```

#### `sprite(path, x, y, width, height, sx, sy, sw, sh, color, alpha)`
Draws a sprite image or colored rectangle.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `path` | string/null | required | Image path (null for rectangle) |
| `x` | number | required | X position |
| `y` | number | required | Y position |
| `width` | number | 32 | Display width |
| `height` | number | 32 | Display height |
| `sx` | number | null | Source X (for sprite sheets) |
| `sy` | number | null | Source Y |
| `sw` | number | null | Source width |
| `sh` | number | null | Source height |
| `color` | string | "#ffffff" | Fallback color |
| `alpha` | number | 1 | Transparency (0-1) |

```rage
sprite("player.png", 100, 100, 32, 32)
sprite("spritesheet.png", 100, 100, 32, 32, sx=64, sy=0, sw=32, sh=32)
```

---

### Color Functions

#### `rgb(r, g, b)`
Creates an RGB color string.

```rage
color = rgb(255, 128, 0)  // Orange
rect(0, 0, 100, 100, rgb(255, 0, 0))
```

#### `rgba(r, g, b, a)`
Creates an RGBA color string with alpha.

```rage
color = rgba(255, 0, 0, 0.5)  // Semi-transparent red
```

#### `hsl(h, s, l)`
Creates an HSL color string.

| Parameter | Range | Description |
|-----------|-------|-------------|
| `h` | 0-360 | Hue |
| `s` | 0-100 | Saturation (%) |
| `l` | 0-100 | Lightness (%) |

```rage
color = hsl(120, 100, 50)  // Pure green
```

#### `hsla(h, s, l, a)`
Creates an HSLA color string with alpha.

```rage
color = hsla(240, 100, 50, 0.5)  // Semi-transparent blue
```

---

### Math Functions

#### Basic Math

| Function | Description | Example |
|----------|-------------|---------|
| `abs(x)` | Absolute value | `abs(-5)` → `5` |
| `floor(x)` | Round down | `floor(3.7)` → `3` |
| `ceil(x)` | Round up | `ceil(3.2)` → `4` |
| `round(x)` | Round to nearest | `round(3.5)` → `4` |
| `min(a, b)` | Minimum of two values | `min(3, 5)` → `3` |
| `max(a, b)` | Maximum of two values | `max(3, 5)` → `5` |
| `clamp(value, min, max)` | Clamp value to range | `clamp(15, 0, 10)` → `10` |
| `sign(x)` | Sign of number (-1, 0, 1) | `sign(-5)` → `-1` |

#### Power and Roots

| Function | Description | Example |
|----------|-------------|---------|
| `sqrt(x)` | Square root | `sqrt(16)` → `4` |
| `pow(base, exp)` | Exponentiation | `pow(2, 3)` → `8` |
| `log(x)` | Natural logarithm | `log(2.718)` ≈ `1` |
| `log10(x)` | Base-10 logarithm | `log10(100)` → `2` |
| `exp(x)` | e^x | `exp(1)` ≈ `2.718` |

#### Trigonometry

| Function | Description |
|----------|-------------|
| `sin(x)` | Sine (radians) |
| `cos(x)` | Cosine (radians) |
| `tan(x)` | Tangent (radians) |
| `asin(x)` | Arc sine |
| `acos(x)` | Arc cosine |
| `atan(x)` | Arc tangent |
| `atan2(y, x)` | Two-argument arc tangent |
| `sinh(x)` | Hyperbolic sine |
| `cosh(x)` | Hyperbolic cosine |
| `tanh(x)` | Hyperbolic tangent |

#### Angle Conversion

| Function | Description | Example |
|----------|-------------|---------|
| `deg(radians)` | Radians to degrees | `deg(3.14159)` ≈ `180` |
| `rad(degrees)` | Degrees to radians | `rad(180)` ≈ `3.14159` |

#### Constants

| Function | Value |
|----------|-------|
| `PI()` | 3.14159... |
| `TAU()` | 6.28318... (2π) |
| `E()` | 2.71828... |

#### Random

| Function | Description | Example |
|----------|-------------|---------|
| `random()` | Random float 0-1 | `random()` → `0.7234...` |
| `randomInt(min, max)` | Random integer (inclusive) | `randomInt(1, 6)` → `4` |

---

### Game Helper Functions

#### `lerp(a, b, t)`
Linear interpolation between two values.

```rage
// Move 10% of the way from current to target each frame
x = lerp(x, target_x, 0.1)
```

#### `distance(x1, y1, x2, y2)`
Calculate distance between two points.

```rage
dist = distance(player.x, player.y, enemy.x, enemy.y)
if (dist < 50) {
  // Collision!
}
```

#### `rect_overlap(x1, y1, w1, h1, x2, y2, w2, h2)`
Check if two rectangles overlap (collision detection).

```rage
if (rect_overlap(player.x, player.y, 32, 32, enemy.x, enemy.y, 32, 32)) {
  // Collision detected!
}
```

---

### Array Functions

#### `array(size)`
Create an array of a given size filled with null.

```rage
grid = array(100)  // 100 null elements
```

#### `len(arr)`
Get the length of an array or string.

```rage
items = [1, 2, 3]
count = len(items)  // 3
text_len = len("hello")  // 5
```

#### `push(arr, value)`
Add an element to the end of an array. Returns the new length.

```rage
scores = []
push(scores, 100)
push(scores, 200)
// scores is now [100, 200]
```

#### `pop(arr)`
Remove and return the last element.

```rage
items = [1, 2, 3]
last = pop(items)  // 3
// items is now [1, 2]
```

#### `insert(arr, index, value)`
Insert a value at a specific index.

```rage
items = [1, 3]
insert(items, 1, 2)  // [1, 2, 3]
```

#### `remove(arr, value)`
Remove the first occurrence of a value. Returns true if found.

```rage
items = [1, 2, 3, 2]
remove(items, 2)  // items is now [1, 3, 2]
```

#### `index(arr, value)`
Find the index of a value (-1 if not found).

```rage
items = ["a", "b", "c"]
idx = index(items, "b")  // 1
```

#### `contains(arr, value)`
Check if array contains a value.

```rage
if (contains(inventory, "key")) {
  // Player has the key
}
```

#### `slice(arr, start, end)`
Get a portion of an array.

```rage
items = [1, 2, 3, 4, 5]
middle = slice(items, 1, 4)  // [2, 3, 4]
```

You can also use slice syntax directly:
```rage
items = [1, 2, 3, 4, 5]
first_three = items[0:3]   // [1, 2, 3]
last_two = items[-2:]      // [4, 5]
without_last = items[:-1]  // [1, 2, 3, 4]
copy = items[:]            // Full copy
```

#### `sort(arr)` / `sorted(arr)`
Sort an array. `sort` modifies in place, `sorted` returns a new array.

```rage
numbers = [3, 1, 4, 1, 5]
sort(numbers)  // numbers is now [1, 1, 3, 4, 5]

original = [3, 1, 4]
new_arr = sorted(original)  // original unchanged
```

#### `reverse(arr)` / `reversed(arr)`
Reverse an array. `reverse` modifies in place, `reversed` returns a new array.

```rage
items = [1, 2, 3]
reverse(items)  // items is now [3, 2, 1]
```

#### `extend(arr, other)`
Add all elements from another array.

```rage
a = [1, 2]
b = [3, 4]
extend(a, b)  // a is now [1, 2, 3, 4]
```

#### `count(arr, value)`
Count occurrences of a value.

```rage
items = [1, 2, 2, 3, 2]
num_twos = count(items, 2)  // 3
```

#### `join(arr, separator)`
Join array elements into a string.

```rage
words = ["hello", "world"]
sentence = join(words, " ")  // "hello world"
```

---

### Input Functions

#### Action-Based Input

Actions are abstract inputs mapped to common controls:

| Action | Keyboard | Description |
|--------|----------|-------------|
| `"left"` | Arrow Left, A | Move left |
| `"right"` | Arrow Right, D | Move right |
| `"up"` | Arrow Up, W | Move up |
| `"down"` | Arrow Down, S | Move down |
| `"jump"` | Space | Jump |
| `"action"` | Enter | Primary action |
| `"a"` | Z | Button A |
| `"b"` | X | Button B |
| `"start"` | Enter | Start/Pause |
| `"select"` | Shift | Select |

#### `pressed(action)`
Returns true on the **frame** the action starts.

```rage
if (pressed("jump")) {
  player.vel_y = -400  // Jump!
}
```

#### `held(action)`
Returns true **while** the action is held.

```rage
if (held("right")) {
  player.x = player.x + speed * dt
}
```

#### `released(action)`
Returns true on the **frame** the action ends.

```rage
if (released("action")) {
  // Fire after releasing button
}
```

#### Raw Key Input

For specific key detection:

#### `key_pressed(key)`
True when a specific key is first pressed.

```rage
if (key_pressed("ArrowLeft")) { ... }
if (key_pressed(" ")) { ... }  // Space
if (key_pressed("a")) { ... }
```

#### `key_held(key)`
True while a specific key is held.

```rage
if (key_held("Shift")) {
  // Run faster
}
```

#### `key_released(key)`
True when a specific key is released.

---

#### Mouse Input

#### `mouse_x()` / `mouse_y()`
Get the current mouse position.

```rage
mx = mouse_x()
my = mouse_y()
circle(mx, my, 5, "#ff0000")  // Cursor
```

#### `mouse_pressed(button)` / `mouse_held(button)` / `mouse_released(button)`
Mouse button input (0=left, 1=middle, 2=right).

```rage
if (mouse_pressed(0)) {
  // Left click
  shoot(mouse_x(), mouse_y())
}
```

---

#### Touch Input

#### `touch_count()`
Number of active touch points.

```rage
if (touch_count() > 0) {
  // Touch detected
}
```

#### `touch_x(index)` / `touch_y(index)`
Get position of a specific touch point.

```rage
if (touch_count() > 0) {
  tx = touch_x(0)
  ty = touch_y(0)
}
```

---

#### Input Buffering (Advanced)

Input buffering allows for more forgiving controls in platformers.

#### `buffer_input(action, duration)`
Buffer an input for the specified duration (seconds).

```rage
if (pressed("jump")) {
  buffer_input("jump", 0.1)  // Buffer for 100ms
}
```

#### `check_buffer(action)`
Check if an action is buffered (consumes the buffer).

```rage
// In update loop, when player lands:
if (player.on_ground and check_buffer("jump")) {
  // Execute buffered jump
  player.vel_y = -400
}
```

#### `peek_buffer(action)`
Check buffer without consuming it.

#### `clear_buffer(action)` / `clear_all_buffers()`
Clear buffered inputs.

#### `buffer_time(action)`
Get remaining buffer time in seconds.

---

### Audio Functions

#### `music(path, volume)`
Play looping background music.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `path` | string/null | required | Audio file path (null to stop) |
| `volume` | number | 5 | Volume level (0-10) |

```rage
music("background.mp3", 5)
music(null)  // Stop music
```

#### `stop_music()`
Stop the current music.

#### `music_volume(volume)`
Set music volume (0-10).

```rage
music_volume(3)  // Lower the music
```

#### `sound(path, gain)`
Play a one-shot sound effect.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `path` | string | required | Audio file path |
| `gain` | number | 5 | Volume (0-10) |

```rage
sound("jump.wav", 5)
sound("explosion.wav", 8)
```

#### `stop_sounds()`
Stop all currently playing sounds.

#### `master_volume(volume)`
Set master volume for all audio (0-10).

---

### Utility Functions

#### `print(...args)`
Print values to the console (for debugging).

```rage
print("Player position:", player.x, player.y)
print("Score:", score)
```

---

## Array Indexing

Arrays support negative indexing (like Python):

```rage
items = [1, 2, 3, 4, 5]
items[0]   // 1 (first)
items[-1]  // 5 (last)
items[-2]  // 4 (second to last)
```

---

## Slice Notation

Arrays and strings support slice notation:

```rage
arr = [1, 2, 3, 4, 5]

arr[1:4]   // [2, 3, 4]
arr[:3]    // [1, 2, 3]
arr[2:]    // [3, 4, 5]
arr[:]     // [1, 2, 3, 4, 5] (copy)
arr[-2:]   // [4, 5]
arr[:-1]   // [1, 2, 3, 4]
```

Works the same for strings:

```rage
s = "hello"
s[1:4]  // "ell"
s[:2]   // "he"
```

---

## The `draw` Block

The `draw` block is called every frame and is where you render graphics:

```rage
draw {
  clear("#000000")
  
  // Draw game objects
  rect(player.x, player.y, 32, 32, "#00ff00")
  
  // Draw UI
  text("Score: " + score, 10, 30, 16, "#ffffff")
}
```

---

## The `update` Block

The `update` block is called every frame with delta time (`dt`) as a parameter:

```rage
update(dt) {
  // dt is the time in seconds since last frame
  // Typically around 0.016 (60 FPS)
  
  // Frame-independent movement
  player.x = player.x + velocity * dt
  
  // Apply gravity
  player.vel_y = player.vel_y + gravity * dt
}
```

Always multiply speeds and accelerations by `dt` to ensure consistent behavior regardless of frame rate.
