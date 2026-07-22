# Simple Shell

A tiny REPL that reads a line, hands it to `/bin/sh -c`, and waits for it to finish. A learning exercise in `fork`/`exec`/`wait`.

## What it does

Prints a `myshell> ` prompt, reads one line of input, and runs it. Each command is executed by forking a child that calls `execvp` on `/bin/sh -c "<your line>"`, while the parent blocks in `wait` until the child exits. Type `exit` to quit.

Because it delegates to `/bin/sh`, you get shell features for free — pipes, redirection, globbing, and built-ins all work, since `sh` is doing the actual parsing.

## Build & run

```sh
gcc main.c -o main
./main
```

The included `.replit` compiles with `gcc $(find . -name '*.c') -o main` and runs `./main`.

## Example

```
myshell> echo hello
hello
myshell> ls -la | wc -l
      12
myshell> exit
```

## Implementation notes

- `fgets` into a fixed 100-byte buffer; the trailing newline is stripped with `strcspn`.
- The child runs `execvp("/bin/sh", {"/bin/sh", "-c", cmd, NULL})`, so command parsing (splitting args, pipes, redirection) is left entirely to `sh`.
- `exit(0)` after `execvp` is a fallback that only runs if `execvp` fails.

## Scope

Practice code, not a real shell. Known limitations:

- No own argument parsing — everything is passed to `/bin/sh`, so this doesn't demonstrate manual tokenizing or building the `argv` for `execvp` yourself.
- 100-byte input buffer with no bounds handling; longer lines get truncated.
- No check for EOF (Ctrl-D) on `fgets`, so closing stdin loops on stale input.
- No `#include <sys/wait.h>` — `wait` works via an implicit declaration, which modern compilers warn about.
- No signal handling, no prompt history, no built-ins beyond `exit`.
