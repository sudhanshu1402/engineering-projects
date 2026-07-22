# Data Structures & Algorithms

C++ practice programs written while learning DSA during college and self-study. Each file is a small standalone program with its own `main()` that you compile and run on its own. Kept public as a learning archive, not a library.

> For active, production-grade work, see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

## What's here

The code is grouped by topic, roughly ordered from fundamentals to data structures. Most files start with a comment block stating the problem and the approach, then implement it and demonstrate it in `main()` with hard-coded sample input.

| Folder | What it covers | Files |
| --- | --- | --- |
| [`fundamental/`](fundamental) | Pointers & references, printing patterns, C++ STL walkthroughs (vector, set, map, stack, queue, deque, list, algorithms), plus Big-O notes. | 22 C++ + notes |
| [`array/`](array) | Array basics: traversal, reverse, min/max, second largest, duplicates, missing element, delete element, prefix sums, count elements greater than x. | 12 C++ |
| [`strings/`](strings) | String handling: length, char/word counts, palindrome, anagram, subsequences, remove spaces, occurrences, naive pattern searching. Folder README also summarizes Naive / Rabin-Karp / KMP / Boyer-Moore. | 14 C++ |
| [`searching/`](searching) | Linear search, binary search (iterative + recursive), first/last/count of a key, integer square root by search, hashing with linear probing. | 8 C++ |
| [`sorting/`](sorting) | Bubble, selection, insertion sort, and merge sort split across a merge function and the divide step. Folder README covers when to use each sort. | 5 C++ |
| [`stack/`](stack) | Stack implemented with a fixed array, plus a second variant. | 2 C++ |
| [`linked-list/`](linked-list) | Singly linked list: build via struct, insert/delete operations, reverse, find middle node. Includes `notes.md`. | 4 C++ |

The `fundamental/` folder breaks down further:

- `pointer/` — pointers, references, pointer-to-array, passing by reference (8 programs)
- `pattern/` — nested-loop shape printing: triangles, inverted, increasing/decreasing (6 programs)
- `cpp-stl/` — one file per STL container/utility (8 programs)
- `complexity/` — time and space complexity notes (`.txt`)

Note: the top-level `fundamental/README.md` is a longer set of DSA notes written in TypeScript (Big-O, patterns, linked lists, trees, heaps, graphs, Dijkstra, DP). The runnable code in this repo is C++.

## Build & run

No build system — each `.cpp` is compiled directly. You need a C++ compiler (`g++` or `clang++`).

```bash
g++ -std=c++17 searching/binary-search.cpp -o binary-search
./binary-search
```

Or compile and run in one step:

```bash
g++ -std=c++17 sorting/merge-divide.cpp -o /tmp/sort && /tmp/sort
```

## Example

`searching/binary-search.cpp` implements binary search both iteratively and recursively over a sorted array, with the sample input baked into `main()`:

```cpp
int array[] = {20, 25, 40, 56, 64, 70, 82};
int key = 21;
// prints -1 / "Element not found!" since 21 isn't in the array
```

Change the array and `key` in `main()` to try other inputs, then recompile.

## Scope

Learning exercises. The programs favor readability and step-by-step comments over generality — inputs are hard-coded, there are no tests, and a few use fixed-size arrays. That's the point: they show the mechanics of each algorithm plainly.
