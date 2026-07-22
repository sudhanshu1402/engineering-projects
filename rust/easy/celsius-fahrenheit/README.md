# Celsius to Fahrenheit

A command-line Rust program that reads a Celsius temperature and prints it in Fahrenheit.

## What it does

Prompts for a Celsius value on stdin, parses it as a floating-point number, applies `C * 1.8 + 32`, and prints the Fahrenheit result. That's the whole program — a beginner exercise for stdin input, string parsing, and basic arithmetic in Rust.

## Stack

- Rust (edition 2021)
- Standard library only (`std::io`) — no external dependencies

## Build & run

```bash
cargo run
```

For a release binary:

```bash
cargo build --release
./target/release/celsius_fahrenheit
```

## Example

```
Enter temp in Celsius:
100
Fahrenheit: 212
```

## Notes

- Input is parsed with `.unwrap()`, so anything that isn't a valid number (e.g. `abc`) will panic. Fine for a learning script; not meant to be robust.
- The manifest file here is named `cargo.toml`. Cargo expects `Cargo.toml`, so on a case-sensitive filesystem you'd need to rename it; on macOS's default case-insensitive filesystem it works as-is.

## Scope

Practice project under `rust/easy`. Deliberately minimal.
