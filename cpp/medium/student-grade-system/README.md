# Student Grade System

A small command-line program that stores students, their grades, and computes each one's average.

## What it does

Runs a menu loop with three options:

1. **Add Student** — enter a name, then type grades one at a time. Enter `-1` to finish. The average is computed on the spot.
2. **Show Report** — prints every student with their average.
3. **Exit** — leaves the loop.

Data lives in memory only; it's gone when the program exits. This is a practice exercise in structs, `std::vector`, and console I/O, not a persistent database.

## Stack

Plain C++17. Standard library only (`<iostream>`, `<vector>`, `<string>`, `<numeric>`, `<algorithm>`). No external dependencies.

## Build and run

```bash
g++ -std=c++17 main.cpp -o main
./main
```

## Example session

```
1. Add Student
2. Show Report
3. Exit
Choice: 1
Enter student name: Ada
Enter grades (-1 to stop): 90 85 100 -1
1. Add Student
2. Show Report
3. Exit
Choice: 2

--- Student Report ---
Name: Ada | Avg: 91.6667
```

## Notes

- Names are read with `std::cin >> name`, so they can't contain spaces (a first name only).
- Average uses `std::accumulate` with a `0.0` seed to force floating-point division.
- A student added with no grades (immediate `-1`) gets an average of `0.0`.
- No input validation on the menu choice — a non-numeric entry will break the loop.
