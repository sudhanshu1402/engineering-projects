# Number Guess

A command-line number guessing game in Go. Practice project.

## What it does

Picks a random number from 1 to 100 and asks you to guess it. After each guess it tells you "Higher" or "Lower", and "Win!" once you get it right. Non-numeric input is silently ignored and it asks again.

## Stack

Go standard library only — no dependencies, no `go.mod`. Uses `bufio` for reading input, `math/rand` for the target, and `strconv` to parse guesses.

## Run

```bash
go run .
```

Or build a binary:

```bash
go build
./number-guess
```

## Example

```
Guess 1-100
Guess: 50
Higher
Guess: 75
Lower
Guess: 62
Higher
Guess: 68
Win!
```

## Notes

- The loop runs until you guess right; there's no attempt limit or quit command (Ctrl+C to exit early).
- `rand.Seed(time.Now().UnixNano())` seeds per run so the target differs each time.
- Small enough to fit in one `main.go`. It's a learning exercise, not a polished tool.
