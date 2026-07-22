# Memory Allocator

A minimal first-fit memory allocator in C++ that hands out chunks from a single fixed buffer. Learning exercise, not a drop-in `malloc`.

## What it does

`SimpleAllocator` grabs one `char[]` buffer up front (1024 bytes in `main`) and tracks it as a list of `Block` records (offset, size, free flag). `allocate` scans the block list for the first free block big enough and returns a pointer into the buffer. `deallocate` finds the block by offset and flips it back to free. Every call prints what happened.

The point is to show the mechanics of a bump/first-fit arena: raw buffer, offset bookkeeping, and pointer arithmetic (`memory + offset` on the way out, `(char*)ptr - memory` on the way back).

## Scope and known limitations

This is a demo, and the code says so in its own comments. Two things are stubbed out:

- **No block splitting.** When a free block is larger than the request, the code computes the leftover block but never inserts it into the vector. So the remaining space is lost — one allocation effectively claims the whole matching block.
- **No coalescing.** `deallocate` marks a block free but doesn't merge adjacent free blocks (the "Merge logic would go here" comment).

Because of the missing split, the buffer behaves as if it holds one block at a time. Running `main` produces:

```
Allocated 100 bytes at offset 0
Allocation failed.
Freed memory at offset 0
Allocated 50 bytes at offset 0
```

The second allocation fails because the first took the only block, and the third succeeds only after the first is freed. That's the honest behavior, not a bug to be surprised by — it's what this version implements.

## Build & run

Standard C++, no dependencies beyond the STL.

```sh
g++ -std=c++17 main.cpp -o main
./main
```

The `.replit` config compiles the same way (`g++ -std=c++17 ... -o main`, then `./main`).

## Where to take it next

If you want a working allocator, the two edits are: actually insert the split-off block into `blocks` after resizing the current one, and in `deallocate` merge with neighboring free blocks. Those two changes turn this from a walkthrough into a usable first-fit arena.
