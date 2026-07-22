# DSA Fundamentals (C++)

Beginner C++ warm-up exercises for learning data structures and algorithms. Small standalone `.cpp` files, each demonstrating one concept: star patterns, pointers and references, the STL containers, and some time-complexity practice questions.

These are learning exercises, not a library. Every file has its own `main()` and runs on its own.

## Layout

| Folder | What's in it |
| --- | --- |
| `pattern/` | Nested-loop star patterns (triangles, inverted, ascending/descending) |
| `pointer/` | Pointers, references, array traversal via pointers, pass-by-reference |
| `cpp-stl/` | STL container demos: `array`, `vector`, `list`, `deque`, `stack`, `queue`, `set`, plus `<algorithm>` helpers |
| `complexity/` | Plain-text notes working through Big-O of sample loops |

## Files

### `pattern/`
Each file hardcodes `n = 5` and prints a star shape with nested `for` loops.

- `increasing.cpp` — left-aligned triangle, growing
- `decreasing-pattern.cpp` — left-aligned triangle, shrinking
- `increasing-triangle.cpp` — centered pyramid
- `decreasing-triangle.cpp` — centered pyramid variant
- `increasing-inverted.cpp` / `desending-inverted.cpp` — inverted variants

### `pointer/`
- `pointer.cpp` — address-of (`&`), dereference (`*`), and printing a pointer's own address
- `array-pointer.cpp` — walking an array by incrementing a pointer
- `refrence.cpp` — references as aliases; includes a (deliberately broken) pass-by-value swap to show it does *not* mutate the caller
- `refrence-pointer.cpp`, `pointer-1.cpp`, `pointer-2.cpp`, `application-erf.cpp` — further pointer/reference practice

Note: `jump.cpp` is an empty placeholder.

### `cpp-stl/`
Short demos of each container's common operations.

- `vector.cpp` — init styles, `push_back`/`pop_back`, `capacity`, `front`/`back`, `size`, `clear`
- `array.cpp` — fixed-size `std::array`
- `list.cpp` — doubly linked list (note on contiguous vs. node-based storage)
- `deque.cpp`, `stack.cpp`, `queue.cpp` — adaptor/sequence containers
- `set.cpp` — `insert`, `erase` via iterator, `find`, iteration
- `algo.cpp` — `binary_search`, `max`, `swap`, `reverse`, `rotate`, `sort`

### `complexity/`
- `time-and-space-complexity.txt` — worked Big-O of loop snippets (e.g. `i *= 2` → O(log n), and why `i /= 2` starting from `n` never terminates).

## Build & run

No build system — compile any file directly:

```sh
g++ pattern/increasing.cpp -o out && ./out
```

Some files include `<bits/stdc++.h>` (a GCC extension), so GCC/`g++` is the safe choice over Clang.

Example — `pattern/increasing.cpp` prints:

```
*
* *
* * *
* * * *
* * * * *
```

## Scope

Practice code. Values are hardcoded, there's no input handling or tests, and a couple of files are stubs or intentionally show the "wrong" way (the swap in `refrence.cpp`) to make a point. Treat it as notes-in-code, not production.
