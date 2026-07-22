# blockchain-rust

A minimal blockchain block written in Rust. It builds a single genesis block and prints its SHA-256 hash.

## What it does

Defines a `Block` struct (`index`, `timestamp`, `data`, `prev_hash`, `hash`) and a `calculate_hash` function that hashes those fields concatenated together with SHA-256. `main` creates the genesis block (index 0, data `"Genesis"`, prev_hash `"0"`) and prints its hash.

That's the whole program. There's no chain yet, no proof-of-work, no validation, no block-appending loop. It's a learning exercise covering the one piece every blockchain starts from: content-addressed hashing of a block.

## Stack

- Rust (edition 2021)
- [`sha2`](https://crates.io/crates/sha2) 0.10 for SHA-256

## Build & run

Cargo needs the manifest named `Cargo.toml`. This repo has it lowercased as `cargo.toml`, so rename it first:

```sh
mv cargo.toml Cargo.toml
cargo run
```

Output:

```
Genesis Hash: <64-char hex digest>
```

For a release binary:

```sh
cargo build --release
```

## How the hash works

```rust
let input = format!("{}{}{}{}", index, timestamp, data, prev_hash);
let mut hasher = Sha256::new();
hasher.update(input);
format!("{:x}", hasher.finalize())
```

The timestamp comes from `SystemTime::now()` in milliseconds, so the genesis hash changes on every run. In a real chain you'd freeze the genesis block or seed it deterministically.

## Notes

- `.replit` compiles with `rustc main.rs` directly instead of Cargo — that path ignores the `sha2` dependency and won't link, so use `cargo run`.
- Scope: practice project. To grow it into an actual chain you'd add a `Vec<Block>`, link each new block's `prev_hash` to the previous block's `hash`, and add a validation pass that recomputes hashes to detect tampering.
