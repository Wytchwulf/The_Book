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
    let x: i32 = 5;
    let x: i32 = x + 1;

    {
        let x: i32 = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

### 3.2. Data Types
