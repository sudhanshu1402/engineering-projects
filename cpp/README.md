# C++ Projects

> Part of my public learning archive. For active, production work see the pinned repos on my [GitHub profile](https://github.com/sudhanshu1402).

Small C++ programs written during college and self-study. Each one is a single `main.cpp` console app that runs on its own. They're organized into four folders by how involved they are: `easy`, `medium`, `hard`, `expert`.

Nothing here is a library or a framework. These are practice exercises covering the basics: I/O, control flow, structs and classes, the STL containers (`vector`, `map`), file streams, and a couple of systems-flavored toys.

## Build & run

Every project is one file with a `main()`. Compile it with g++ (the `.replit` config in each folder uses `-std=c++17`):

```bash
cd easy/simple-calculator
g++ -std=c++17 main.cpp -o main
./main
```

Most are menu-driven and read from stdin, so just follow the prompts.

## Projects

### easy

| Project | What it does |
| --- | --- |
| [01-hello-world](easy/01-hello-world) | Placeholder folder — README only, no source yet. |
| [simple-calculator](easy/simple-calculator) | Reads an operator and two numbers, does one arithmetic operation via a `switch`. |
| [unit-converter](easy/unit-converter) | Converts a temperature between Celsius and Fahrenheit based on a `C`/`F` suffix. |
| [stopwatch](easy/stopwatch) | A `Stopwatch` class using `<chrono>`; type `s`/`e`/`q` to start, stop, and print elapsed milliseconds. |

### medium

| Project | What it does |
| --- | --- |
| [student-grade-system](medium/student-grade-system) | Stores students in a `vector<Student>`, reads grades until `-1`, and reports each student's average using `std::accumulate`. |
| [scientific-calculator](medium/scientific-calculator) | Menu of 14 operations — arithmetic, power/sqrt, trig and inverse trig, natural and base-10 log — over `<math.h>`. |

### hard

| Project | What it does |
| --- | --- |
| [bank-management](hard/bank-management) | In-memory accounts kept in a `map<int, BankAccount>`; create accounts by ID and deposit, withdraw, or check balance. |
| [college-management-system](hard/college-management-system) | Student records CRUD backed by a binary file (`College.txt`), with bubble-sort ordering and search by registration number. Written for Windows (`system("CLS")`, `gets`), so it won't compile cleanly on modern toolchains without edits. |

### expert

| Project | What it does |
| --- | --- |
| [memory-allocator](expert/memory-allocator) | A `SimpleAllocator` over a raw `char[]` buffer with a block list and first-fit `allocate`/`deallocate`. Block splitting and free-block merging are stubbed out — it demonstrates the idea, not a working allocator. |
| [trading-simulator](expert/trading-simulator) | Toy market of three stocks with random price drift; buy shares against a cash balance and view your portfolio. |

## Scope

These are learning exercises, not products. Error handling is minimal, input is assumed well-formed, and the "expert" label reflects the topic (allocators, market simulation) rather than the depth of the implementation. The `college-management-system` in particular uses old Windows/C idioms that won't build unchanged on Linux or macOS.
