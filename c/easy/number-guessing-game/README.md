# Number Guessing Game

A tiny C command-line game: the computer picks a random number from 1 to 100 and you guess it, with "Higher!" / "Lower!" hints until you get it.

## What it does

- Seeds the random generator with the current time, then picks a number between 1 and 100.
- Reads your guess each round with `scanf`.
- Tells you whether the target is higher or lower than your guess.
- Counts attempts and prints the total when you guess correctly.

It's a practice exercise for loops, `rand()`/`srand()`, and basic stdin handling in C. Nothing fancy — one file, about 30 lines.

## Build & run

Needs a C compiler (`gcc` or `clang`).

```sh
gcc main.c -o main
./main
```

## Example

```
Guess a number between 1 and 100
Enter your guess: 50
Lower!
Enter your guess: 25
Higher!
Enter your guess: 37
Lower!
Enter your guess: 31
You guessed it in 4 attempts!
```

## Notes

- No input validation: typing a non-number leaves `guess` unchanged and `scanf` keeps failing on the same bad input, so the loop spins. Enter integers only.
- Uses a `do...while` loop, so you always make at least one guess.
