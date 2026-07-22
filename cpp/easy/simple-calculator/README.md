# Simple Calculator

A command-line calculator in C++. Reads an operator and two numbers, prints the result. A beginner practice exercise.

## What it does

It asks for an operator (`+`, `-`, `*`, `/`) and two operands, then uses a `switch` on the operator to compute and print the result. Anything other than those four operators prints an error message. That's the whole program (`main.cpp`, ~38 lines).

Operands are read as `float`, so decimals work.

## Build & run

Needs a C++ compiler (g++ or clang++).

```bash
g++ -std=c++17 main.cpp -o main
./main
```

## Example

```
Enter operator: +, -, *, /: *
Enter two operands: 6 7
6 * 7 = 42
```

## Notes

- No input validation beyond the operator check. Non-numeric input for the operands will fail silently, and `/ 0` produces `inf` (float division), not a caught error.
- Runs once and exits. There's no loop for repeated calculations.
- Scope is intentionally small: it's a switch-statement and basic I/O drill, not a real calculator app.
