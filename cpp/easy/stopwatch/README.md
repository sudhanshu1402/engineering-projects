# Stopwatch

A command-line stopwatch in C++. Type `s` to start timing, `e` to stop and see the elapsed milliseconds, `q` to quit.

## What it does

Wraps a small `Stopwatch` class around `std::chrono::high_resolution_clock`. On start it records a timestamp; on stop it records another and prints the difference in milliseconds. The main loop reads single-character commands from stdin until you quit.

It's a practice piece for learning `<chrono>` timing and basic class design in C++. Nothing fancy.

## Build & run

Compiled with C++17:

```sh
g++ -std=c++17 main.cpp -o main
./main
```

## Example session

```
Enter 's' to start, 'e' to end, 'q' to quit: s
Stopwatch started.
Enter command: e
Stopwatch stopped.
Duration: 4213 ms
Enter command: q
```

## Notes

- `start()` and `stop()` guard on the `running` flag, so a second `s` while already running (or `e` while stopped) is ignored.
- `running` is a `std::atomic<bool>`, though the program is single-threaded — `<thread>` and `<atomic>` are included but not actually used for concurrency here.
- Duration is measured with `high_resolution_clock` and truncated to whole milliseconds via `duration_cast`.
