# Unit Converter

A small C++ command-line program that converts a temperature between Celsius and Fahrenheit.

## What it does

You type a number and a unit letter (`C` or `F`). It prints the value converted to the other scale. That's the whole program right now — a practice exercise in reading mixed input (`std::cin >> temp >> type`) and branching on the unit.

The name is aspirational: `main()` has a `// Add more conversions here` comment, so temperature is the one converter implemented so far.

## Build & run

Needs a C++17 compiler (g++ or clang++).

```bash
g++ -std=c++17 main.cpp -o main
./main
```

The `.replit` config uses the same setup (`g++ -std=c++17`, output binary `main`).

## Example

```
=== Unit Converter ===
Enter temperature (e.g., 32 F or 100 C): 100 C
100 C = 212 F
```

```
Enter temperature (e.g., 32 F or 100 C): 32 F
32 F = 0 C
```

Any letter that isn't C/F (case-insensitive) prints `Invalid unit.`

## Notes

- Formulas: C→F is `temp * 9/5 + 32`; F→C is `(temp - 32) * 5/9`. Division is done as `9.0/5.0` so it stays floating-point.
- Input is read as `double`, so decimals like `98.6 F` work.
- Scope: a learning toy, single file, no error handling beyond the unit check. If you feed it non-numeric input, `std::cin` fails silently.
