# C Projects

> Part of my public learning archive. For active, production-grade work see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

C and C++ code written during college and self-study. Small, single-file console programs that cover the fundamentals: pointers, structs, file I/O, and a couple of Unix system-call exercises (`fork`/`exec`, sockets). Kept public for transparency, not as polished software.

## How it's organized

Projects are grouped into folders by rough difficulty. Each project is its own directory with a `main.c` (or `main.cpp`), a `.replit` config, and a per-project README.

### easy

| Project | What it does |
|---|---|
| [`01-hello-world`](easy/01-hello-world) | Placeholder starter entry — README only, no source. |
| [`number-guessing-game`](easy/number-guessing-game) | Picks a random 1–100 number; loops on `scanf` guesses with higher/lower hints and an attempt count. |
| [`calendar`](easy/calendar) | C++ program that prints a formatted month calendar, with leap-year handling and day-of-week alignment. |

### medium

| Project | What it does |
|---|---|
| [`phonebook-system`](medium/phonebook-system) | In-memory contact store (fixed array of 100 `struct Contact`) with add/search/list via a menu. |
| [`voting-system`](medium/voting-system) | Menu-driven vote casting across four hard-coded candidates plus spoiled votes, then a tally report. |

### hard

| Project | What it does |
|---|---|
| [`bank-system`](hard/bank-system) | Account records persisted to a binary file (`bank.dat`) using `fwrite`/`fread`; create and list accounts. |
| [`hospital-management`](hard/hospital-management) | Patient records (`id`, `name`, `disease`) written to a file with `fwrite`; add and view entries. |

### expert

| Project | What it does |
|---|---|
| [`simple-shell`](expert/simple-shell) | Minimal REPL shell: reads a line, `fork`s, and runs it via `/bin/sh -c` with `execvp`; `exit` to quit. |
| [`web-server`](expert/web-server) | Bare TCP socket server on port 8080 that returns a fixed `HTTP/1.1 200 OK` "Hello world!" response. |

## Build & run

Most projects are a single file. From a project directory:

```bash
# C projects
gcc main.c -o app && ./app

# calendar (C++)
g++ main.cpp -o calendar && ./calendar
```

`web-server` and `simple-shell` use POSIX headers (`sys/socket.h`, `unistd.h`), so they need a Unix-like environment. Test the web server with:

```bash
gcc main.c -o server && ./server &
curl localhost:8080
```

Each folder also has a `.replit` file, so any project can be opened and run directly on Replit.

## Scope note

These are learning exercises. Inputs are trusted (no validation on `scanf`), buffers are fixed-size, and error handling is minimal. They exist to practice C fundamentals, not to be reused as libraries.
