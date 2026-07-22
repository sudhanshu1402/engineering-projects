# Hello World (C++)

The first slot in the C++ practice track. A place to write the canonical
`std::cout << "Hello, World!"` program and confirm the toolchain compiles and runs.

## Status

No source file yet — this directory currently holds only this README. The code
below is the intended starting point.

## The program

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!\n";
    return 0;
}
```

Save it as `hello.cpp` in this directory.

## Build & run

Any C++ compiler works. With g++ or clang++:

```bash
g++ hello.cpp -o hello
./hello
```

Expected output:

```
Hello, World!
```

## Scope

A learning exercise, nothing more — the smallest program that proves the compiler,
linker, and standard library are wired up correctly before moving on to real work.
