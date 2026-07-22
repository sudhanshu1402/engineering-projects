# Console Calculator

A tiny C# console app that reads two numbers and prints their sum and difference. A practice piece for basic input/output and arithmetic.

## What it does

Prompts for two numbers, reads them from the console, and writes out `num1 + num2` and `num1 - num2`. Both are parsed as `double`, so decimals work.

## Stack

Plain C# (.NET). No dependencies beyond the standard library. Configured to run under `dotnet` via the `.replit` file.

## Run

```bash
dotnet run
```

## Example

```
Simple Calculator
Enter number 1: 12.5
Enter number 2: 4
Sum: 16.5
Diff: 8.5
```

## Notes

- Input is parsed with `Convert.ToDouble`, which throws on non-numeric input — no validation or retry loop.
- Only addition and subtraction are implemented; no multiplication, division, or operator selection.

Scope: a learning exercise, not a general-purpose calculator.
