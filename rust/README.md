# Rust

> Part of my public learning archive. For active, production-grade work see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

Small Rust programs I wrote while learning the language, from college and self-study. The focus was getting comfortable with ownership, borrowing, pattern matching, and the crate ecosystem, so most of these are deliberately short. A couple of the harder ones are scaffolds rather than finished apps, and I've marked those honestly below.

## How it's organized

Projects are grouped into four folders by difficulty. Each project is its own Cargo package with a `cargo.toml` and `src/main.rs`.

| Project | Level | What it does | Crates |
| --- | --- | --- | --- |
| [celsius-fahrenheit](easy/celsius-fahrenheit) | easy | Reads a Celsius value from stdin and prints Fahrenheit. | std only |
| [guessing-game](easy/guessing-game) | easy | The classic guess-the-number loop with too-high/too-low hints. | `rand` |
| [calculator](medium/calculator) | medium | Parses a `num op num` expression (e.g. `5 + 10`) and prints the result. | std only |
| [to-do-cli](medium/to-do-cli) | medium | Menu-driven CLI to add and list tasks held in a `HashMap` for the session. | `serde`, `serde_json` |
| [file-compressor](hard/file-compressor) | hard | Gzip-compresses `input.txt` to `output.gz` and prints how long it took. | `flate2` |
| [chat-server](hard/chat-server) | hard | Async TCP echo server on `127.0.0.1:8080`, one task per connection. | `tokio` |
| [blockchain-rust](expert/blockchain-rust) | expert | Builds a genesis block and prints its SHA-256 hash. | `sha2` |
| [async-executor](expert/async-executor) | expert | Scaffold of a single-threaded future executor (`Task`/`Spawner`/queue). | `futures` |

## Running any of them

Each folder is a standalone package. From inside a project directory:

```bash
cargo run
```

For `file-compressor`, put a file named `input.txt` next to where you run it first; it writes `output.gz`. For `chat-server`, connect with something like `nc 127.0.0.1 8080` after it starts and anything you type comes back to you.

## Honest scope notes

- `to-do-cli` keeps tasks in memory only. It pulls in `serde`/`serde_json` but does not actually persist to disk yet.
- `chat-server` is an echo server: each client sees its own messages back, not a broadcast to other clients. It's the tokio accept/read/write loop, not a full chat room.
- `blockchain-rust` creates one genesis block. There's no chain, mining, or validation beyond hashing.
- `async-executor` currently prints a banner from `main`; the `Executor`/`Spawner` types are defined but the poll loop is left as a scaffold.
- The manifest files are named lowercase `cargo.toml`. Cargo expects `Cargo.toml`, so on a case-sensitive filesystem you'd rename them before building.

These are learning exercises, kept public for transparency about how I got here.
