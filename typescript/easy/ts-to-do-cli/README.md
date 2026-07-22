# TS ToDo CLI

A tiny interactive to-do list that runs in the terminal. Type commands, it keeps a list in memory.

This is a practice exercise for learning TypeScript and Node's `readline`. It's ~27 lines in a single file. Nothing is persisted — the list lives only for the session and is gone when you exit.

## What it does

Starts a prompt loop and reads commands from stdin:

- `add <text>` — add an item to the list
- `list` — print the current list
- `exit` — quit

Anything else prints `Unknown` and re-prompts.

## Stack

- TypeScript
- Node.js `readline` (built-in, no dependencies)

There's no `package.json` in this folder. The `.replit` file references `npm install && npm start`, but there are no npm scripts or dependencies defined, so run it directly with a TS runner or compile it first.

## Run it

With [ts-node](https://typestrong.org/ts-node/) (no build step):

```bash
npx ts-node index.ts
```

Or compile with `tsc` and run the output:

```bash
tsc index.ts
node index.js
```

## Example session

```
Command (add/list/exit): add buy milk
Added
Command (add/list/exit): add call dentist
Added
Command (add/list/exit): list
[ 'buy milk', 'call dentist' ]
Command (add/list/exit): exit
```

## Notes

- `list` uses `console.log(todos)`, so it prints the raw array (with brackets and quotes) rather than a formatted list.
- The `add ` check requires a trailing space — `add` alone falls through to `Unknown`.
- Storage is an in-memory `string[]`; there's no delete, edit, or save-to-disk.

## Scope

Learning project, kept deliberately minimal. It's the smallest thing that demonstrates a command loop over stdin in TypeScript.
