# Rust Book Study Guide

This repo is my follow along for the [Rust Book](https://rust-book.cs.brown.edu/) from Brown University's CS department.

## Table of Contents

- [Chapters](#chapters)
  - [Chapter 1: Getting Started](#chapter-1-getting-started)
  - [Chapter 2: Programming a Guessing Game](#chapter-2-programming-a-guessing-game)
  - [Chapter 3: Common Programming Concepts](#chapter-3-common-programming-concepts)
      - [3.1. Variables and Mutability](#3.1-variables-and-mutability)
      - [3.2. Data Types](#3.2-data-types)
      - [3.3. Functions](#3.3-functions)
      - [3.4. Comments](#3.4-comments)
      - [3.5. Control Flow](#3.5-control-flow)
  - [Chapter 4: Understanding Ownership](#chapter-4-understanding-ownership)
  - [Chapter 5: Using Structs to Structure Related Data](#chapter-5-using-structs-to-structure-related-data)
  - [Chapter 6: Enums and Pattern Matching](#chapter-6-enums-and-pattern-matching)
  - [Chapter 7: Managing Growing Projects with Packages, Crates, and Modules](#chapter-7-managing-growing-projects-with-packages-crates-and-modules)
  - [Chapter 8: Common Collections](#chapter-8-common-collections)
  - [Chapter 9: Error Handling](#chapter-9-error-handling)
  - [Chapter 10: Generic Types, Traits, and Lifetimes](#chapter-10-generic-types-traits-and-lifetimes)
  - [Chapter 11: Writing Automated Tests](#chapter-11-writing-automated-tests)
  - [Chapter 12: An I/O Project: Building a Command Line Program](#chapter-12-an-io-project-building-a-command-line-program)

## Chapter 1: Getting Started

```rust
fn main() {
    println!("Hello, world!");
}
```

## Chapter 2: Programming a Guessing Game

```rust
use std::io;
use std::cmp::Ordering;
use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    loop {
        println!("Please input your guess");

        let mut guess = String::new(); 

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed {}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Guess Higher!"),
            Ordering::Greater => println!("Guess Lower!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

## Chapter 3: Common Programming Concepts

### 3.1. Variables and Mutability

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

```rust
fn main() {
    let x: = 5;
    let x: = x + 1;

    {
        let x: = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

### 3.2. Data Types

- Integer Types
```rust
fn main() {
let guess: u32 = "42".parse().expect("Not a number!");
}
```
- Floating-Point Types 
```rust
fn main() {
    let x = 2.0; // f64

    let y: f32 = 3.0; // f32
}
```
- Numeric Operations
```rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // Results in -1

    // remainder
    let remainder = 43 % 5;
}
```
- Boolean Type
```rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```
- Char Type
```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```
- Compound Type -- Tuple
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```
```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```
- Compound Type -- Array
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```
```rust
fn main() {
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
}
```
```rust
fn main() {
let a: [i32; 5] = [1, 2, 3, 4, 5];
}
```

### 3.3 Functions

```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```
```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {}", x)
}
```
```rust
fn main() {
    print_labeled_measurements(5, 'h');
}

fn print_labeled_measurements(value: i32, unit_label: char) {
    println!("The measurement is: {value}{unit_label}");
}
```
```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```

### 3.4 Comments

```rust
fn main() {
// So we’re doing something complicated here, long enough that we need
// multiple lines of comments to do it! Whew! Hopefully, this comment will
// explain what’s going on.
}
```
```rust
fn main() {
/* So we’re doing something complicated here, long enough that we need
   multiple lines of comments to do it! Whew! Hopefully, this comment will
   explain what’s going on. */
}
```

### 3.5 Control Flow

- Conditionals
```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```
- Loops -- loop
```rust
fn main() {
    loop {
        println!("again!");
    }
}
```
```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```
- Loops -- while
```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```
- Loops -- for
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```
```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```

