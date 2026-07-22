# Linked List

Singly linked list practice in C++. Each file is a standalone program that builds a list and runs one operation, written while learning the data structure.

## Files

| File | What it does |
|------|--------------|
| `list-using-struct.cpp` | Builds a 3-node list by hand (`node` struct with a constructor) and prints it. The minimal starting point. |
| `list-operations.cpp` | A `LinkedList` class with insert-at-start, insert-at-end, insert-at-position, search, delete-by-value, and display. The main reference file. |
| `mid-node.cpp` | Finds the middle node using the slow/fast (tortoise-hare) pointer trick. |
| `reverse-list.cpp` | Reverses a list in place with the three-pointer (prev/current/next) loop, plus a recursive print. |
| `notes.md` | Insertion diagrams and a to-do list of linked-list problems to solve next. |

## Build & run

Each file has its own `main()`, so compile and run them one at a time:

```sh
g++ list-operations.cpp -o list-operations && ./list-operations
```

Same pattern for the others (`g++ <file>.cpp -o out && ./out`).

## Example

`list-operations.cpp` builds `7 3 1 9` from the front, appends `10 60 100`, inserts `500` at positions 3 and 7, then deletes and searches:

```
Current Linked List: 7 3 1 500 9 10 60 500 100
Deleting 1 Deleting 500
Searching for 7: 1
Searching for 13: 1
7 3 9 10 60 100
```

## Notes

- The middle-node and reverse solutions are the ones worth studying: fast/slow pointer and the in-place three-pointer reversal are the standard patterns for these problems.
- These are learning exercises, not a reusable library. A few rough edges are left in on purpose from when they were written:
  - `list-operations.cpp` contains stray `@_aj7t` handle tokens in the source that will stop it compiling until removed.
  - `remove()` in `list-operations.cpp` deletes the head before reading `head->next`, which is use-after-free for the head case.
  - `mid-node.cpp` has no constructor, so `head` is uninitialized before the first insert.
- `notes.md` lists the follow-up problems still to do: odd/even list, remove duplicates, merge sort, palindrome check, loop detection, and remove Nth from end.

Part of the `dsa` section of the engineering-projects portfolio.
