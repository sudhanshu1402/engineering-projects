# chat-server

An async TCP echo server in Rust. Every byte a client sends is written straight back to it.

## What it actually is

Despite the name, this isn't a multi-client chat room. It's a per-connection echo server built on Tokio:

- Binds to `127.0.0.1:8080`.
- Accepts connections in a loop.
- Spawns a Tokio task per connection.
- Reads into a 1 KB buffer and writes the same bytes back, until the client disconnects (read returns 0) or an error occurs.

It's a learning exercise for async networking — `TcpListener`, `tokio::spawn`, and the async read/write traits. There's no broadcast between clients, no message framing, no protocol. Each connection only talks to itself.

## Stack

- Rust (edition 2021)
- [Tokio](https://tokio.rs/) 1.x with the `full` feature set

## Build & run

```bash
cargo run                    # debug build, starts the server
cargo build --release        # optimized binary at target/release/chat_server
```

The dependency manifest is committed as `cargo.toml` (lowercase). Cargo expects `Cargo.toml`, so on a case-sensitive filesystem you'll need to rename it before building:

```bash
mv cargo.toml Cargo.toml
```

## Usage

Start the server, then connect with any TCP client. Using `nc`:

```bash
cargo run &
nc 127.0.0.1 8080
hello
hello        # echoed back
```

Each line you type comes straight back. Open a second `nc` in another terminal and it gets its own independent echo session — the two connections don't see each other.

## Implementation notes

- The whole server is ~20 lines in `src/main.rs`.
- Concurrency comes from `tokio::spawn` — the accept loop never blocks on a slow client, since each connection runs on its own task.
- Reads use a fixed `[0; 1024]` stack buffer per task; anything larger than 1 KB is echoed in chunks across loop iterations.
- Errors (read or write failure) just drop the connection by returning from the task.

## Scope

Practice code, not a real chat service. To make it live up to the name you'd add shared state (a list of connected clients or a broadcast channel), message framing, and a way to fan messages out to everyone instead of echoing back to the sender.
