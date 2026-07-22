# Number Guess

A console number-guessing game in C#. Practice exercise.

## What it does

The program picks a random integer from 1 to 100 and asks you to guess it. After each guess it tells you:

- `Higher` if your guess is below the target
- `Lower` if your guess is above the target
- `You Win!` when you hit it, then exits

The loop runs until you guess correctly. There's no guess counter and no upper limit on attempts.

## Stack

Plain C# on .NET. No external packages. `.replit` is set up to run it on Replit with `dotnet run`.

## Run it

```bash
dotnet run
```

## Example

```
Guess a number between 1 and 100
Guess: 50
Higher
Guess: 75
Lower
Guess: 62
You Win!
```

## Notes

- Input is parsed with `Convert.ToInt32(Console.ReadLine())`. Non-numeric input (or Ctrl+D / empty input) will throw and crash — there's no validation. Fine for a toy; would need a `TryParse` guard for anything real.
- `new Random()` seeds from the system clock, so each run gets a different target.

Scope: a small learning piece, not a polished game.
