---
layout: doc
title: Support Structure
description: Understanding how character supports work in Ragelang
order: 3
---

# Support Structure

In Ragelang, every character in your code must be supported by characters beneath it. Unsupported characters will fall until they hit something or fall out of the program entirely.

## Basic Rules

### Foundation

The foundation is marked by `#` characters on a single line. Everything above the foundation must be supported. The foundation itself never falls.

```rage
print("Hello")
######################
```

**Important:** The `#` characters must be outside of strings. `#` characters inside strings (between quotes) are treated as regular characters, not foundation markers.

### Support Rules

A character is supported if there is a non-space character in one of these positions directly below it:

1. **Directly below** (same column)
2. **One column to the left** below
3. **One column to the right** below

Support is **recursive** - a character can only support others if it is itself supported. This means you need a chain of support all the way down to the foundation.

```rage
// The shape below works, while this comment is not supported and will collapse
//   |
//  /|\
//   |
######################
```

### Falling Behavior

- Characters fall **straight down** in their own column
- Characters fall until they hit another character or fall out of the program
- Processing happens from **bottom to top**, one line at a time
- Space characters don't count as support - they're ignored

### Example

```rage
// Unsupported characters will fall
print("Hello")
// . . . . . .
##############
```

In this example, the `.` characters provide support for the code above. Without them, the `print` statement would fall.

## Tips and Tricks

### 1. Cover Your Longest Row

Cover your longest row with supports on top to catch any falling supports from above that may extend too far.

```rage
// Some comment that overreaches the supports below
//  ..........................................
// Long function call that needs protection ............
result = calculate_complex_value(x, y, z, width, height)
// .....................................................
########################################################
```

By placing supports above the longest line, you ensure that any supports falling from above will land safely.

### 2. Use Small Characters

Use `.` or another small character to be less noisy on the eyes. While `|` works well, `.` can be less visually distracting.

```rage
fun update_player(dt) {
 player.x += speed * dt
 player.y += gravity * dt
} // ....................
// .....................
#######################
```

### 3. Single Space Indent

Use a single space indent in code blocks, so you don't have to put an intentionally misaligned comment on top of all your code.

```rage
 fun my_function() {
  x = 10 //.........
  y = 20 // ........
 } // ..............
// .................
####################
```

With single-space indentation, your support line can align naturally with the code, rather than needing a special offset comment line under the function before your code.

### 4. Build Angles

Use the left-right support to your advantage, and build angles from your longer lines down to make it a bit more readable.

```rage
// Long line of code that needs support
very_long_function_name_with_many_parameters(param1, param2, param3)
// ................................................................
// ...............................................................
// ..............................................................
// .............................................................
// ............................................................
// ...........................................................
// ..........................................................
// .........................................................
// ........................................................
// .......................................................
// ......................................................
// .....................................................
// ....................................................
pretty_long_function_name_that_is_just_a_bit_shorter()
######################
```

By using diagonal supports, you can create a more visually organized support structure that's easier to read and maintain.


## What Happens When Characters Fall?

When unsupported characters fall:

1. They fall straight down in their column
2. They stop when they hit another character
3. If they fall past the foundation, they're removed from the program
4. The resulting code may still be valid Ragelang, but it might not do what you intended!

This can lead to subtle bugs - your code might run, but produce unexpected results because characters have moved around.

If you are clever, you may even intentionally let some characters fall, and obfuscate the real intent of your program!
