# async-executor

A scaffold for a hand-rolled async task executor in Rust — the skeleton of the classic "build your own runtime" exercise.

## What this is

The starting point for writing a minimal `Future` executor from scratch, the way `tokio` or `async-std` work under the hood but stripped to the essentials. It sets up the type plumbing:

- `Executor` — owns the receiving end of a channel of ready-to-poll tasks.
- `Spawner` — holds the sending end; `spawn()` boxes a future into a `Task` and pushes it onto the queue.
- `Task` — an `Arc`-wrapped future plus a handle to re-queue itself when woken.
- `new_executor_and_spawner()` — wires the two halves together over a bounded `sync_channel` (capacity 10,000).

The polling loop itself — the part that pulls tasks off the queue, builds a `Waker`, calls `Future::poll`, and re-schedules on `Poll::Pending` — is **not implemented**. `main` just prints a banner:

```
Async Executor Scaffold
```

This is the honest state of the file: struct definitions and the spawn path are real; the run loop is a stub (`// ... Implementation details omitted ...`).

## Stack

- Rust (edition 2021)
- `futures = "0.3"` is declared as a dependency but not yet referenced in the code — it's there for the `ArcWake` helper you'd reach for when finishing the executor.

Standard library pieces already in use: `std::future::Future`, `std::pin::Pin`, `std::task::{Context, Poll, Waker}`, `std::sync::{Arc, Mutex}`, and `std::sync::mpsc::sync_channel`.

## Build & run

```sh
cargo run                    # runs the scaffold, prints the banner
cargo build --release        # release binary
```

There's also a `src/.replit` set up to compile `main.rs` directly with `rustc` (no Cargo), which drops the `futures` dependency.

## What's left to make it real

To turn this into a working executor:

1. Implement `ArcWake` for `Task` so a woken task re-sends itself on `task_sender`.
2. Add `Executor::run()` — loop over `ready_queue.recv()`, lock the task's future, build a `Context` from the task's waker, and `poll` it; put the future back if it returns `Pending`.
3. In `main`, create the pair, spawn a future or two, drop the spawner, and call `run()`.

## Scope

Learning exercise, and currently a partial one. Filed under `rust/expert` because a full executor touches pinning, wakers, and manual `Future` polling — but as it stands this is scaffolding, not a runnable runtime.
