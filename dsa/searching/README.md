# Searching

Practice C++ programs for classic searching problems: linear search, binary search, and the common binary-search variants (first/last occurrence, count of a key, integer square root). Written while learning DSA, so most files carry both a naive approach and a better one side by side.

## What's here

Each file is a standalone program with its own `main()` that runs a hardcoded example. There's no shared library or build system — every file compiles and runs on its own.

| File | Problem | Approaches shown |
|------|---------|------------------|
| `linear-search.cpp` | Is a key present in an (unsorted) array? | Linear scan; returns a 1/0 found flag |
| `binary-search.cpp` | Find a key's index in a sorted array | Iterative + recursive binary search |
| `first-occurence.cpp` | Index of the first occurrence of a repeated key | Naive scan + binary search (move left on match) |
| `last-occurence.cpp` | Index of the last occurrence of a repeated key | Naive reverse scan, recursion, binary search (move right on match) |
| `first-and-last-occurence.cpp` | First and last index of a key | Single linear pass tracking both |
| `count-key.cpp` | How many times a key appears | Naive count, recursion, and `(last - first) + 1` |
| `square-root.cpp` | Integer (floor) square root of a number | Linear increment until `i*i > a` |
| `hashing-linear-probing.cpp` | Hash-table insert with linear probing | Stub / work in progress (see note below) |

## Build & run

Compile any single file with g++ and run it:

```bash
g++ binary-search.cpp -o binary-search
./binary-search
```

`square-root.cpp` reads from stdin: first the number of test cases `T`, then one integer per case.

```bash
g++ square-root.cpp -o square-root
echo "2
16
20" | ./square-root
# prints 4 then 4 (floor sqrt)
```

Every other file uses a hardcoded array inside `main()`, so it prints its result with no input. To try a different case, edit the array/key at the top of `main()` and recompile.

## Example

`first-occurence.cpp` searches `{5, 5, 5, 6, 6, 8, 9, 9, 9}` for `9`:

```
6
The first occurrence of element 9 is located at index 6
```

The naive scan and the binary-search version both land on index 6 — the binary version keeps moving `high` left after a match to find the leftmost hit.

## Notes

- The binary-search variants only work on **sorted** arrays. `linear-search.cpp` works on any array.
- The first/last-occurrence binary searches are the standard trick: on a match, don't stop — keep going left (for first) or right (for last) to find the boundary.
- `count-key.cpp` shows the neat shortcut once you have both boundaries: the count is `last - first + 1`.

## Rough edges

This is learning code, and a few files are unfinished or buggy — left as-is rather than polished:

- `hashing-linear-probing.cpp` doesn't compile. It's a skeleton with an empty probing loop, and `LinearProbing()` is called with no arguments. Treat it as a TODO, not a working example.
- `binary-search.cpp`'s recursive `bSearch` passes `start` instead of `end` into the right-half call, so the right-side recursion is wrong.
- `last-occurence.cpp`'s naive `findIndex` starts its loop at `i = N`, which reads one past the end of the array. The `main()` there also computes the binary-search result but never prints it.
- `count-key.cpp`'s recursive version calls the iterative `countTotal` instead of recursing on itself, and has an unreachable `return` after it.

If you're reading these to learn, prefer the iterative versions — they're the ones that behave correctly.
