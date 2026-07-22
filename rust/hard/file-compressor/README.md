# file-compressor

Gzip-compresses a file and prints how long it took. A small Rust exercise in streaming I/O with `flate2`.

## What it does

Reads `input.txt`, writes a gzip-compressed `output.gz`, and prints the elapsed time. That's the whole program — about 15 lines in `src/main.rs`.

It streams the data instead of loading the whole file into memory: `std::io::copy` pumps bytes from a `BufReader` straight into a `GzEncoder`, so file size isn't bounded by RAM.

## Stack

- Rust (edition 2021)
- [`flate2`](https://crates.io/crates/flate2) 1.0 — DEFLATE/gzip encoding, at `Compression::default()`

## Build & run

The input and output paths are hardcoded, so you need an `input.txt` next to where you run it.

```sh
echo "some text to compress" > input.txt
cargo run
```

Output:

```
Compressed in 1.2ms
```

You get an `output.gz` in the working directory. Verify it:

```sh
gunzip -k output.gz && diff input.txt output
```

For a release binary:

```sh
cargo build --release
./target/release/file_compressor
```

## Notes

- Paths (`input.txt`, `output.gz`) and the compression level are fixed in source. No CLI args yet — changing files means editing `main.rs`.
- Errors are handled with `.unwrap()`, so a missing `input.txt` panics rather than printing a friendly message.
- The build manifest is `cargo.toml` (lowercase). Cargo expects `Cargo.toml`, so rename it if `cargo run` can't find the package.
- The `src/.replit` file compiles `main.rs` directly with `rustc`, bypassing Cargo — a leftover from a Replit setup.

## Scope

Practice project. The obvious next steps are reading paths from `argv`, exposing the compression level, and returning `Result` instead of unwrapping.
