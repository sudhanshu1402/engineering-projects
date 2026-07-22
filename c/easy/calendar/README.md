# Calendar

A command-line program that prints a full 12-month calendar for any year you type in.

## What it does

You give it a year, it computes which weekday January 1st falls on, then walks through all twelve months and prints each one as a grid under a `S M T W T F S` header. Leap years are handled, so February shows 28 or 29 days correctly.

It's a small learning exercise in C++: date math, loops, and formatted console output. Nothing fancy, no external input files, no persistence.

## How it works

A few short functions carry the logic:

- `leap_year(year)` — standard Gregorian rule: divisible by 4, but not 100 unless also 400.
- `start_day(year)` — figures out the weekday of Jan 1 by counting leap days since year 1 (`(year + (year-1)/4 - (year-1)/100 + (year-1)/400) % 7`). Returns 0–6.
- `number_days_month(m, leap)` — day count per month, February depending on `leap`.
- `print_month(days, weekDay)` — prints the day numbers, wrapping to a new line after Saturday. It takes `weekDay` by reference and carries it forward, so each month continues from where the last one ended.

The starting weekday flows month to month through the year via that reference parameter, which is the one non-obvious part of the code.

## Build & run

Despite living under `c/`, the source is C++ (`main.cpp`, uses `<iostream>` and `<iomanip>`). Compile with g++:

```sh
g++ main.cpp -o calendar
./calendar
```

`makefile.win` is a Dev-C++ generated makefile targeting MinGW on Windows (produces `Calendar.exe`); it isn't needed on Linux/macOS.

Note: the included `.replit` config compiles `*.c` files, which won't pick up `main.cpp` — use the g++ command above directly.

## Example

```
Enter the year : 2024

         2024
       January
 S  M  T  W  T  F  S
____________________
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
...
```

(Each month prints in turn down to December.)

## Scope

Practice project. The output alignment is fixed-width and assumes a terminal, month names and the weekday layout are hardcoded, and there's no input validation beyond an error-and-exit path in the day-count function. Fine for what it is: a self-contained calendar printer.
