# Guessing Game

A command-line number-guessing game in Rust. The classic exercise from Chapter 2 of *The Rust Programming Language* ("the book").

## What it does

Picks a random secret number between 1 and 100, then loops asking you to guess. Each guess prints "Too small!", "Too big!", or "You win!" and exits on a correct guess. Non-numeric input is silently ignored — you just get asked again.

## Stack

- Rust (edition 2021)
- [`rand`](https://crates.io/crates/rand) 0.8.5 — for the random secret number

## Build & run

```sh
cargo run
```

For an optimized binary:

```sh
cargo build --release
./target/release/guessing_game
```

Note: the manifest here is named `cargo.toml` (lowercase). Cargo expects `Cargo.toml`, so rename it if `cargo` can't find the package.

## Example

```
Guess the number!
Please input your guess.
50
Too big!
Please input your guess.
25
Too small!
Please input your guess.
37
You win!
```

## Implementation notes

- Input parsed with `guess.trim().parse::<u32>()`; a `Err` result hits `continue`, so garbage input never crashes the game — it just loops.
- `rand::thread_rng().gen_range(1..=100)` uses an inclusive range, so both 1 and 100 are reachable.
- `read_line` errors are handled with `.expect(...)`, which panics on I/O failure rather than recovering.

## Scope

Learning exercise. No tests, no config, no bells. It's here to practice Rust basics: `loop`, `match`, shadowing (`guess` is rebound from `String` to `u32`), and pulling in an external crate.
