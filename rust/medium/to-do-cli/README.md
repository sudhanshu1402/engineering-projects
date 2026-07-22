# to-do-cli

A tiny interactive to-do list that runs in the terminal. Practice project for learning Rust basics.

## What it does

Runs a loop with a three-option menu:

```
1. Add
2. List
3. Exit
```

- **Add** prompts for a task and stores it.
- **List** prints every stored task with its numeric id.
- **Exit** breaks the loop and quits.

Tasks live in a `HashMap<usize, String>` in memory. There's no persistence — close the program and everything is gone. Ids are assigned as `map.len() + 1`, so they're stable only if you never delete anything (there's no delete).

## Stack

- Rust (edition 2021)
- `serde` and `serde_json` are listed in `cargo.toml` but not actually used in the code yet — presumably left in for a future "save to JSON file" step.

## Build & run

```bash
cargo run                    # run it
cargo build --release        # release binary at target/release/todo_cli
```

## Example session

```
1. Add
2. List
3. Exit
1
Enter task:
buy milk
1. Add
2. List
3. Exit
1
Enter task:
call dentist
1. Add
2. List
3. Exit
2
1: buy milk
2: call dentist
1. Add
2. List
3. Exit
3
```

Note: `HashMap` iteration order isn't sorted, so with more items the list won't necessarily print in id order.

## Scope

Learning exercise, not a real tool. It covers `loop`, `match`, reading stdin, and a `HashMap`. No persistence, no delete/edit, no error handling beyond `.unwrap()` on stdin reads. The obvious next steps would be wiring in the serde deps to save tasks to disk and adding delete/complete actions.
