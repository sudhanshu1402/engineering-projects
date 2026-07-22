# Hello World (C)

The classic first C program. This is the entry slot in the `c/easy` practice set.

## Status

Placeholder — no source file has been added to this directory yet. It currently
contains only this README. Once a `hello.c` lands here, the notes below apply.

## What it is meant to be

A minimal program that prints `Hello, World!` to standard output and exits. It's
a warm-up exercise: confirm the toolchain compiles and runs, nothing more.

Expected source (`hello.c`):

```c
#include <stdio.h>

int main(void) {
    printf("Hello, World!\n");
    return 0;
}
```

## Build & run

Once `hello.c` exists, compile with any C compiler:

```bash
cc hello.c -o hello
./hello
```

Expected output:

```text
Hello, World!
```

## Scope

Learning exercise. No dependencies, no build system, no tests — a single
translation unit and the standard library.
