# Scientific Calculator

A menu-driven console calculator in C++. Pick an operation by number, type your input, get one answer.

## What it does

On start it prints a menu of 14 operations grouped into three columns:

- Basic: division, multiplication, subtraction, addition, exponent (`pow`), square root
- Trigonometric: sin, cos, tan, and their inverses (asin, acos, atan)
- Logarithmic: natural log, log base 10

You enter the number for the operation you want, then the operand(s). Binary ops (1-5) ask for two numbers; the rest ask for one. It computes the result, prints it, and exits. There's no loop — one calculation per run.

It's a practice project for `switch` control flow and the C `<math.h>` functions, not a general expression evaluator.

## Stack

Plain C++ (`<iostream>`, `<math.h>`), no external libraries. Ships with a Dev-C++ 5.11 project (`makefile.win`, `.dev`, `.layout`) and a Replit config.

## Build & run

Anywhere with g++:

```sh
g++ main.cpp -o calc
./calc
```

Replit (from `.replit`):

```sh
g++ -std=c++17 *.cpp -o main
./main
```

Windows with Dev-C++ / MinGW (from `makefile.win`), produces `Scientific Calculator.exe`:

```sh
mingw32-make -f makefile.win
```

## Example

```
Enter the function that you want to perform : 5
Enter the number : 2
Enter the exponent : 10
Exponent = 1024
```

```
Enter the function that you want to perform : 14
Enter the number : 1000
Log with base 10 = 3
```

## Things worth knowing

- The trig functions (7-9) take the angle in **radians** — `sin`, `cos`, `tan` are called on the raw input. But the inverse trig functions (10-12) convert their result **to degrees** (`* 180.0 / PI`). So input is radians one way, output is degrees the other. Inconsistent, but that's what the code does.
- Values are stored as `float`, so results carry single-precision rounding.
- No input validation: dividing by 0, `sqrt` of a negative, or `log` of a non-positive number will produce `inf` / `nan` rather than an error. Typing a non-menu number just prints `Wrong Input`.
- Angle inputs to the inverse functions outside `[-1, 1]` give `nan`.

## Scope

Toy learning exercise. Single-shot, no loop, no error handling — a straightforward tour of a menu-driven `switch` and the standard math functions.
