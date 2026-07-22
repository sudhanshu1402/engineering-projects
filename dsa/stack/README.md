# Stack (C++)

Array-backed stack implementation while learning the LIFO data structure.

## What's here

- **`stack-array.cpp`** — a `Stack` class backed by a fixed-size `int` array (`MAX = 10`). Implements `push`, `pop`, `peek`, and `isEmpty`, with overflow/underflow guards. `main()` runs a small driver: pushes 10, 20, 30, peeks, checks empty, then pops.
- **`stack.cpp`** — notes and loose snippets (the four core operations written out as bare statements). Not a compilable program; it's a scratch file for the concept, linked to a [Techie Delight article](https://medium.com/techie-delight/stack-data-structure-practice-problems-and-interview-questions-9f08a35a7f19).

## Build & run

```bash
g++ stack-array.cpp -o stack-array
./stack-array
```

Expected output:

```
10 pushed into stack
20 pushed into stack
30 pushed into stack
Element at top is : 30
0
```

(The `0` is `isEmpty()` returning false.)

## Notes

- Uses `#include <bits/stdc++.h>`, a GCC-specific header — fine for practice, not portable to non-GCC compilers.
- Fixed capacity of 10; `push` prints `Stack Overflow` past that. `pop`/`peek` on an empty stack print a message and return `0`.
- `peek()` is declared to return `int` but doesn't return a value on the success path — a bug worth noting if you reuse this code.

## Scope

Learning exercise, not a library. Single-type (`int`), fixed-size, prints results to stdout instead of exposing a clean API.
