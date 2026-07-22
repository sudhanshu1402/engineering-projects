# Strings (C++ practice)

Small, single-file C++ programs I wrote while learning how strings work in DSA. Each file solves one classic string problem, usually with a naive version and a faster version side by side so the difference is easy to see. Inputs are hard-coded in `main()`, so you compile a file and run it.

## Tech

- C++ (STL: `std::string`, `sort`, `reverse`, `substr`, `find`)
- Some files include `<bits/stdc++.h>` (works with g++; not portable to all compilers)
- No build system, no deps. One file = one program.

## Build & run

```sh
g++ anagram.cpp -o anagram
./anagram
```

Swap in any filename. To change the input, edit the strings in that file's `main()` and recompile.

## What's in here

| File | Problem | Approaches |
|------|---------|-----------|
| `input-output.cpp` | Read/print a string | `cin.get`, plus commented `cin>>` and `getline` |
| `string-intro.cpp` | STL basics | `length`, concat, `substr`, `find`, compare, iterate |
| `string-functions.cpp` | Length via a helper fn | `str.length()`; notes on `strlen`/`strcmp`/`strcpy` |
| `length-string.cpp` | Count spaces | single loop |
| `count-words.cpp` | Count words | count spaces + 1 |
| `count-char.cpp` | Classify chars | ASCII ranges → upper / lower / digit / special |
| `remove-spaces.cpp` | Strip spaces in place | two-pointer over a C string |
| `palindrone.cpp` | Palindrome check | reverse-and-compare, and two-pointer |
| `anagram.cpp` | Anagram check | sort-and-compare O(n log n), count array O(n) |
| `anagram-string.cpp` | Anagram check (variant) | same two methods, `count[256]` |
| `left-most-repetion.cpp` | Leftmost repeating char | O(n²) brute force, and count-array pass |
| `sub-sequence.cpp` | Is one string a subsequence of another | two-pointer scan |
| `word-occurrences.cpp` | Count occurrences of a word | scan + `substr` compare |
| `pattern-searching.cpp` | Find all positions of a pattern | naive brute force + a sliding variant |

## Notes on the approaches

- The **count-array** trick (anagram, leftmost-repeating) uses a fixed `int count[256]` indexed by the character's ASCII value. It turns an O(n²) scan into O(n) with O(1) extra space, at the cost of assuming 8-bit chars.
- **Palindrome** and **subsequence** both use the two-pointer pattern — the workhorse move for these problems.
- `README`'s notes on Rabin-Karp, KMP, and Boyer-Moore describe faster pattern-matching algorithms; the code here only implements the naive O(mn) search.

## Known rough edges

These are learning drafts, not polished code. A few real bugs to be aware of:

- **`anagram.cpp` / `anagram-string.cpp`**: the count-array method increments on `str1`/`str2` in the same loop without first checking equal length, so it can read out of bounds when lengths differ. `anagram.cpp` guards length before that method; `anagram-string.cpp`'s `str1[i] || str2[i]` length check is not a valid one.
- **`left-most-repetion.cpp`**: `leftMostRepeated` indexes `count[str[i]]` in the second loop (should iterate the string and return the first char with count > 1), and falls off the end with no `return`.
- **`pattern-searching.cpp`**: both loops use `i < n - m` (misses a match at the last valid position) and `naiveSearching`'s inner loop runs to `n` instead of `m`. Treat the output as illustrative, not correct.
- Several helpers declared `int` return nothing (they `cout` instead) — fine for a scratch file, not for reuse.

## Scope

Practice exercises. The point was to get reps on string manipulation and to compare naive vs. optimized thinking, not to ship a library. Read them as worked examples.

## ASCII quick reference

```
digits 48–57   |   A–Z 65–90   |   a–z 97–122
```
