---
layout: doc
title: Language Reference
description: Complete reference for Ragelang syntax and features
order: 2
---

This is the complete reference for Ragelang's syntax and features.

## Comments

```
// Single line comment

/* 
   Multi-line 
   comment 
*/
```

## Variables

```
let x = 10
let name = "Ragelang"
let active = true
```

## Functions

```
fn greet(name) {
    print("Hello, " + name + "!")
}

fn add(a, b) {
    return a + b
}
```

## Control Flow

### If/Else

```
if condition {
    // do something
} else if other_condition {
    // do something else
} else {
    // fallback
}
```

### Loops

```
// While loop
while condition {
    // loop body
}

// For loop
for i in 0..10 {
    print(i)
}
```

## Data Types

- **Numbers**: `42`, `3.14`
- **Strings**: `"Hello, World!"`
- **Booleans**: `true`, `false`
- **Arrays**: `[1, 2, 3]`

*More features coming as development progresses!*

