# Array

Basic array problems in C++, solved while learning DSA. Each file is a standalone `main()` program you compile and run on its own.

## What's here

Small, self-contained solutions to common array questions. Nothing is a library or shared between files — every `.cpp` has its own `main()`. Some read input from the keyboard (`cin`), others use a hardcoded array inside the file.

| File | Problem | Input |
|------|---------|-------|
| `input-output.cpp` | Read 5 numbers into an array and print them back | stdin |
| `find-min-max.cpp` | Find the min and max of `n` numbers | stdin |
| `max-min.cpp` | Same min/max, tracking the index instead of the value | hardcoded |
| `largest-element.cpp` | Largest and smallest element — both the O(n²) brute-force and the O(n) single-pass versions | hardcoded |
| `second-largest.cpp` | Second largest element in one pass | hardcoded |
| `reverse-array.cpp` | Reverse an array in place with two pointers | hardcoded |
| `duplicates.cpp` | Remove duplicates from a sorted array, return the count removed | hardcoded |
| `repeate-element.cpp` | Count how many times a given value `x` appears | hardcoded + stdin |
| `greater-than-x.cpp` | Count elements strictly greater than `x` | hardcoded |
| `missing-element.cpp` | Find the one missing number in `1..n` using the sum formula | stdin |
| `prefix-sum-array.cpp` | Build the prefix-sum array | stdin |
| `delete-element.cpp` | Delete the element at a given index by shifting left | hardcoded |

## Build and run

Compile any file with `g++` and run the binary:

```bash
g++ find-min-max.cpp -o find-min-max
./find-min-max
```

For the stdin programs (`find-min-max`, `missing-element`, `prefix-sum-array`, `input-output`, `repeate-element`), type the count first, then the numbers. Example for `find-min-max`:

```
5
4 1 9 2 7
```

prints:

```
1
9
```

The hardcoded ones just run:

```bash
g++ reverse-array.cpp -o reverse-array && ./reverse-array
# 1 7 6 3 0
```

## Notes

- `missing-element.cpp` reads `n` elements but uses `(n+1)(n+2)/2` for the expected sum, so it treats the range as `1..n+1` — read the code before feeding it input.
- `largest-element.cpp` keeps both a naive nested-loop approach and the efficient single-pass one side by side on purpose: it's a comparison of the two.
- A few files call their functions with a size that doesn't match the array's real length (e.g. `getLargest(arr, 4)` on a 5-element array). These are practice snapshots, not polished code.

## Scope

Learning exercises, not production code. Fixed-size arrays, `using namespace std`, and no error handling throughout. The goal was to get the array patterns into muscle memory, not to build a library.
