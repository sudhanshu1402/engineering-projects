# Calculator

A command-line calculator in Rust. Reads one expression from stdin and prints the result.

## What it does

You type something like `5 + 10`, it parses the three whitespace-separated parts (number, operator, number) and prints the answer. Supports `+`, `-`, `*`, `/`. Any unknown operator returns `0`.

It's a learning exercise for Rust basics: reading stdin, splitting strings, parsing to `f64`, and pattern matching with `match`.

## Stack

Plain Rust, no dependencies. `std::io` for input. Edition 2021.

## Build & run

```
cargo run
```

For a release binary:

```
cargo build --release
```

## Usage

```
$ cargo run
Enter expression (e.g. 5 + 10):
5 + 10
Result: 15
```

Numbers are parsed as `f64`, so `7 / 2` gives `3.5`.

## Notes

- Input must be exactly `number operator number` with spaces between each part. `5+10` (no spaces) won't parse.
- No error handling. Bad input, missing parts, or non-numbers will panic (the code uses `.unwrap()` and indexes `parts[0..2]` directly).
- Division by zero yields `inf` rather than an error, since it's float division.
- An unrecognized operator falls through the `match` to `0.0`.

This is a toy. It's here to practice the language, not to be a robust calculator.
