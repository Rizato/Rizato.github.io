---
layout: doc
title: Language Reference
description: Complete reference for Ragelang syntax and features
order: 2
---

# Language Reference

This document provides a complete reference for the Ragelang programming language, including all built-in functions, control flow structures, and language features.

## Table of Contents

- [Basic Syntax](#basic-syntax)
- [Data Types](#data-types)
- [Variables](#variables)
- [Operators](#operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Enums and Pattern Matching](#enums-and-pattern-matching)
- [Built-in Functions](#built-in-functions)
- [Canvas and Screen](#canvas-and-screen)
- [Scene Management](#scene-management)

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
- Enum definitions
- A `draw` block (for rendering)
- An `update` block (for game logic)

```rage
// Variables
player_x = 100
player_y = 200
// Functions .
fun move_player(dx, dy) {
 player_x = player_x + dx
 player_y = player_y + dy
} // ...........................................
// Draw block - called every frame for rendering
draw { // ......................................
 clear("#000000") // ...........................
 circle(player_x, player_y, 20, "#ff0000") // ..
} // ...............................................
// Update block - called every frame with delta time
update(dt) { // ....................................
 // Game logic here ................................
} //................................................
// .................................................
####################################################
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
| `&&` | Logical AND | `x > 0 && x < 10` |
| `||` | Logical OR | `x < 0 || x > 10` |
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

### Increment and Decrement Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `++` | Increment by 1 | `x++` or `++x` |
| `--` | Decrement by 1 | `x--` or `--x` |

**Prefix vs Postfix:**
- **Prefix** (`++x`): Increments first, then returns the new value
- **Postfix** (`x++`): Returns the current value, then increments

---

## Control Flow

### If / Else

Conditional execution with `if`, `else if`, and `else`:

```rage
if (score > 100) {
 text("High score!", 10, 10, 16, "#00ff00")
} else if (score > 50) {
 text("Good score!", 10, 10, 16, "#ffff00")
} else {
 text("Keep trying!", 10, 10, 16, "#ffffff")
}
```

### Loops

#### Infinite Loop with Break

```rage
i = 0
loop {
 if (i >= 10) {
  break
 }
 print(i)
 i++
}
```

### Match Expressions

Pattern matching with `match`:

```rage
result = match value {
 1 => "one",
 2 => "two",
 _ => "other"
}
```

See [Enums and Pattern Matching](#enums-and-pattern-matching) for more details.

---

## Functions

Functions are defined with the `fun` keyword:

```rage
fun add(a, b) {
 return a + b
}

result = add(5, 3)  // 8
```

Functions can have default parameters and keyword arguments:

```rage
fun greet(name, greeting = "Hello") {
 return greeting + ", " + name
}

greet("World")                    // "Hello, World"
greet("World", greeting="Hi")     // "Hi, World"
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

| Constant | Value |
|----------|-------|
| `PI` | 3.14159... |
| `TAU` | 6.28318... (2π) |
| `E` | 2.71828... |

#### Random

| Function | Description | Example |
|----------|-------------|---------|
| `random()` | Random float 0-1 | `random()` → `0.7234...` |
| `randomInt(min, max)` | Random integer (inclusive) | `randomInt(1, 6)` → `4` |

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

### Input Functions

Ragelang provides multiple ways to handle input: action-based input (abstracted controls), raw key input, mouse input, and touch input. Action-based input is recommended for most games as it automatically handles keyboard and gamepad input.

#### Action-Based Input

Actions are abstract inputs that map to multiple input methods (keyboard, gamepad). This makes your game work with both keyboard and gamepad without additional code.

**Available Actions:**

| Action | Keyboard | Gamepad | Description |
|--------|----------|---------|-------------|
| `"left"` | Arrow Left, A | D-Pad Left, Left Stick Left | Move left |
| `"right"` | Arrow Right, D | D-Pad Right, Left Stick Right | Move right |
| `"up"` | Arrow Up, W | D-Pad Up, Left Stick Up | Move up |
| `"down"` | Arrow Down, S | D-Pad Down, Left Stick Down | Move down |
| `"jump"` | Space | A/Cross Button | Jump |
| `"interact"` | E | X/Square Button | Interact/Use |
| `"start"` | Escape | Start Button | Start/Pause menu |

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

For specific key detection when you need to check individual keys rather than actions. Use key names as defined by the [KeyboardEvent.key](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key) API.

**Common Key Names:**
- Arrow keys: `"ArrowLeft"`, `"ArrowRight"`, `"ArrowUp"`, `"ArrowDown"`
- Letters: `"a"`, `"b"`, `"c"`, etc. (lowercase)
- Numbers: `"0"`, `"1"`, `"2"`, etc.
- Special keys: `"Space"`, `"Enter"`, `"Escape"`, `"Shift"`, `"Control"`, `"Alt"`
- Function keys: `"F1"`, `"F2"`, etc.

#### `key_pressed(key)`
Returns `true` on the frame a specific key is first pressed.

```rage
if (key_pressed("ArrowLeft")) {
 // Left arrow just pressed
}
if (key_pressed(" ")) { ... }  // Space bar
if (key_pressed("a")) { ... }  // 'a' key
if (key_pressed("Escape")) {
 // Open menu
}
```

#### `key_held(key)`
Returns `true` while a specific key is held down.

```rage
if (key_held("Shift")) {
 // Run faster while shift is held
 speed = base_speed * 2
}
```

#### `key_released(key)`
Returns `true` on the frame a specific key is released.

```rage
if (key_released("Space")) {
 // Space bar was just released
}
```

#### Mouse Input

Mouse input provides position and button state. The coordinates are relative to the canvas element.

#### `mouse_x()` / `mouse_y()`
Get the current mouse position in pixels, relative to the canvas.

```rage
mx = mouse_x()
my = mouse_y()
circle(mx, my, 5, "#ff0000")  // Draw cursor
```

**Note:** Mouse position is only accurate when the mouse is over the canvas element.

#### `mouse_pressed(button)` / `mouse_held(button)` / `mouse_released(button)`
Mouse button input. Returns `true` for the specified button state.

| Button | Value | Description |
|--------|-------|-------------|
| Left | `0` | Primary mouse button |
| Middle | `1` | Middle mouse button (scroll wheel click) |
| Right | `2` | Right mouse button |

```rage
if (mouse_pressed(0)) {
 // Left click just happened
 shoot(mouse_x(), mouse_y())
}

if (mouse_held(0)) {
 // Left button is being held
 drag_item(mouse_x(), mouse_y())
}

if (mouse_released(0)) {
 // Left button was just released
 drop_item()
}
```

#### Touch Input

Touch input is designed for mobile devices and touchscreens. Touch coordinates are relative to the canvas element.

#### `touch_count()`
Returns the number of active touch points (fingers on screen).

```rage
if (touch_count() > 0) {
 // At least one finger is touching the screen
 text("Touch detected!", 10, 10, 16, "#ffffff")
}

// Multi-touch support
if (touch_count() >= 2) {
 // Two or more fingers - pinch gesture?
}
```

#### `touch_x(index)` / `touch_y(index)`
Get the position of a specific touch point. The `index` parameter specifies which touch point (0 = first touch, 1 = second touch, etc.).

```rage
if (touch_count() > 0) {
 // Get position of first touch
 tx = touch_x(0)
 ty = touch_y(0)
 circle(tx, ty, 10, "#00ff00")
}

// Handle multiple touches
if (touch_count() >= 2) {
 touch1_x = touch_x(0)
 touch1_y = touch_y(0)
 touch2_x = touch_x(1)
 touch2_y = touch_y(1)
 // Calculate distance between touches for pinch gesture
}
```

**Note:** Always check `touch_count()` before accessing touch positions. Accessing a touch index that doesn't exist will return 0.

#### Input Buffering (Advanced)

Input buffering is a technique used in platformers to make controls feel more responsive. It allows players to press a button slightly before they're able to perform the action, and the input will be "remembered" for a short time.

**Common Use Cases:**
- **Jump buffering**: Press jump slightly before landing, and the jump executes when you land
- **Coyote time**: Allow jumping for a short time after leaving a platform
- **Input queuing**: Queue up actions that can't be performed immediately

#### `buffer_input(action, duration)`
Buffer an input for the specified duration (in seconds). The input will be available for checking until the duration expires.

```rage
if (pressed("jump")) {
 buffer_input("jump", 0.1)  // Buffer for 100ms
}
```

**Typical buffer durations:**
- Jump buffering: 0.1-0.15 seconds
- Action queuing: 0.2-0.3 seconds

#### `check_buffer(action)`
Check if an action is buffered and **consumes** the buffer (removes it). Returns `true` if the action was buffered, `false` otherwise.

```rage
// In update loop, when player lands:
if (player.on_ground and check_buffer("jump")) {
 // Execute buffered jump
 player.vel_y = -400
 clear_buffer("jump")  // Optional: clear after use
}
```

**Important:** `check_buffer()` consumes the buffer. If it returns `true`, the buffer is removed and won't be available on the next check.

#### `peek_buffer(action)`
Check if an action is buffered **without consuming** it. Returns `true` if buffered, but leaves the buffer intact.

```rage
if (peek_buffer("jump")) {
 // Jump is buffered, but don't consume it yet
 // Maybe show a visual indicator
}
```

#### `clear_buffer(action)` / `clear_all_buffers()`
Clear specific or all buffered inputs.

```rage
// Clear a specific buffered action
clear_buffer("jump")

// Clear all buffered inputs (useful when changing game states)
clear_all_buffers()
```

#### `buffer_time(action)`
Get the remaining buffer time in seconds for a specific action. Returns `0` if the action is not buffered or has expired.

```rage
remaining = buffer_time("jump")
if (remaining > 0) {
 // Jump is still buffered, show countdown
 text("Jump buffered: " + round(remaining * 100) + "ms", 10, 10, 16, "#ffff00")
}
```

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

### Utility Functions

#### `print(...args)`
Print values to the console (for debugging).

```rage
print("Player position:", player.x, player.y)
print("Score:", score)
```

#### `time()`
Returns time since epoch in seconds.

#### `frames()`
Returns number of frames that have been rendered.

---

## Canvas and Screen

### `width()` / `height()`
Get the canvas dimensions in pixels.

```rage
center_x = width() / 2
center_y = height() / 2
```

---

## Scene Management

### `load_scene(path)`
Loads a new rage script, resetting the current runtime. The path is relative to the game's asset directory.

```rage
if (player.health <= 0) {
 load_scene("assets/rage/game-over.rage")
}
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

The `draw` block is called every frame and is where you render graphics.
You should not modify data in the draw block, because it does not give the delta time.

Ragelang is single threaded, so it's not a hard rule, but it does result in a a smoother game in most cases.

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
