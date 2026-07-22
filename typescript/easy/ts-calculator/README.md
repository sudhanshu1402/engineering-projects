# TS Calculator

A one-function arithmetic calculator in TypeScript. Practice exercise.

## What it is

`index.ts` has a single `calculate(a, b, op)` function that switches on an
operator string (`+`, `-`, `*`, `/`) and returns the result. Anything else
returns `0`. The file runs two example calls and logs them:

```
5 + 3 = 8
10 / 2 = 5
```

That's the whole thing — a learning snippet for TypeScript basics (typed
params, `switch`, return types).

## Run it

No `package.json` here, so run the file directly with a TS runner:

```bash
npx tsx index.ts
# or
npx ts-node index.ts
```

Or compile and run the JS:

```bash
npx tsc index.ts && node index.js
```

## Notes

- `default` case returns `0`, so an unknown operator silently gives `0`
  rather than erroring.
- Division by zero returns `Infinity` (or `NaN` for `0/0`) — standard JS
  number behavior, not handled specially.
- The `.replit` file runs `npm install && npm start`, which won't work as-is
  without a `package.json`; use the commands above instead.

Scope: toy practice code, not a real calculator app.
