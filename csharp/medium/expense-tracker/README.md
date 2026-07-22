# Expense Tracker

A console loop that adds expense amounts to a list and prints the running total. A C# practice exercise.

## What it does

Runs a menu in an infinite loop:

- `1` — prompts for an amount and appends it to an in-memory `List<decimal>`.
- `2` — sums the list and prints the total.

That's the whole program. Nothing is saved: the list lives in memory and is gone when the process exits.

## Stack

- C# on .NET (`Console` I/O only, no external packages).

## Run

```
dotnet run
```

Configured to run this way via `.replit`.

## Example

```
1. Add Expense
2. View Total
1
Amount: 12.50
1. Add Expense
2. View Total
1
Amount: 7.25
1. Add Expense
2. View Total
2
Total: 19.75
```

## Notes / scope

- No exit option — the `while(true)` loop never breaks; stop it with Ctrl+C.
- No input validation. A non-numeric amount throws on `Convert.ToDecimal`, and any menu input other than `1` or `2` is silently ignored.
- Uses the `decimal` type, which is the right choice for money (avoids the rounding error of `float`/`double`).

Toy project for practicing C# console basics — not built for real use.
