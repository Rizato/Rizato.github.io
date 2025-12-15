---
layout: doc
title: TODO
description: Example programs written in Ragelang
order: 3
---

Here are some example programs to help you learn Ragelang.

## Hello World

The classic first program:

```
fn main() {
    print("Hello, World!")
}
```

## FizzBuzz

A programming classic:

```
fn main() {
    for i in 1..101 {
        if i % 15 == 0 {
            print("FizzBuzz")
        } else if i % 3 == 0 {
            print("Fizz")
        } else if i % 5 == 0 {
            print("Buzz")
        } else {
            print(i)
        }
    }
}
```

## Factorial

Calculate factorial recursively:

```
fn factorial(n) {
    if n <= 1 {
        return 1
    }
    return n * factorial(n - 1)
}

fn main() {
    print(factorial(5))  // Output: 120
}
```

## Fibonacci

Generate Fibonacci numbers:

```
fn fib(n) {
    if n <= 1 {
        return n
    }
    return fib(n - 1) + fib(n - 2)
}

fn main() {
    for i in 0..10 {
        print(fib(i))
    }
}
```

*More examples will be added as we develop the game!*

