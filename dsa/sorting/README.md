# Sorting

![](http://www.equestionanswers.com/c/images/sorting-objects.png)

Practice implementations of classic sorting algorithms in C++. These are learning
exercises: single-file programs, each with its own `main()` and a hardcoded test
array. Nothing here is a library — the point was to write the algorithms by hand
and see them run.

## What's in here

| File | Algorithm | Notes |
|------|-----------|-------|
| `bubble-sort.cpp` | Bubble sort | Standard two-loop version, swaps adjacent out-of-order pairs. |
| `selection-sort.cpp` | Selection sort | Swap-heavy variant — swaps on every smaller element found instead of tracking a min index and swapping once (the `min_idx` logic is commented out). Still sorts correctly, just does extra swaps. |
| `insertion-sort.cpp` | Insertion sort | Shifts elements down via swaps until each value lands in place. |
| `merge-function.cpp` | Merge step | Two ways to merge two arrays: a naive one (concatenate then `std::sort`) and a proper two-pointer merge. Prints the result, doesn't return it. |
| `merge-divide.cpp` | Split + merge | Splits one array into left/right halves and merges them with the two-pointer method. Demonstrates the divide step, not a full recursive merge sort. |

## Build & run

Each file is standalone. Compile with any C++ compiler:

```sh
g++ bubble-sort.cpp -o bubble-sort
./bubble-sort
```

The files use `#include <bits/stdc++.h>`, which is a GCC extension — build with
`g++`/`clang` on Linux or macOS. It won't compile with MSVC as-is.

## Example

`bubble-sort.cpp` sorts a fixed array:

```cpp
int arr[] = {64, 34, 25, 12, 22, 11, 90};
```

Output:

```
Sorted array:
11 12 22 25 34 64 90
```

To sort your own data, edit the array in `main()` and recompile.

## Rough edges

Honest notes, since these are practice files:

- The merge programs **print** the merged output rather than writing it back to an
  array, so they can't be composed into a real recursive merge sort as written.
- `merge-function.cpp`'s two-pointer `mergeFunction` uses `while (i < m || j < n)`
  and then reads `a[i]`/`b[j]` unconditionally — once one side is exhausted it can
  read out of bounds before the cleanup loops run. It happens to work on the sample
  inputs but the loop condition should be `&&`.
- Selection sort does more swaps than necessary (see table above).

## Reference notes

Quick notes on when each algorithm is worth using (broader than what's coded here):

- **Quick sort** — no stability needed, average case matters more than worst case.
  O(N log N) average, O(N²) worst, O(log N) stack space.
- **Merge sort** — when you need a stable O(N log N) sort. Costs O(N) extra space.
  Databases use external merge sort for data too large to fit in memory (fewer disk I/Os).
- **Heap sort** — no stability needed, worst-case guarantee matters. O(N log N)
  guaranteed, O(1) extra space.
- **Insertion sort** — small N, or as the base case inside quick/merge sort. O(N²)
  but tiny constant and stable.
- **Bubble / selection sort** — quick-and-dirty only; easiest to hand-write.
- **Counting / radix / bucket sort** — non-comparison sorts that beat O(N log N)
  under specific constraints (limited integer range, few digits, uniform distribution).
