# Compiler Transpiler

A skeleton showing the two front-end stages of a compiler in TypeScript: a tokenizer and a parser. This is a stub, not a working compiler.

## What's here

`compiler.ts` sketches the classic pipeline shape:

- `tokenize(input)` — turns source text into `Token[]` (`{ type, value }`).
- `parse(tokens)` — turns tokens into an AST node (`{ type: 'Program', body: [] }`).

Both are stubbed. `tokenize` ignores its input and always returns a single `let` keyword token; `parse` always returns an empty program. The file ends by running the pipeline on `"let x = 10;"` and printing the result.

## Run it

There's no `package.json` here, so use `ts-node` or compile with `tsc` directly:

```bash
npx ts-node compiler.ts
# or
npx tsc compiler.ts && node compiler.js
```

Output:

```
{ type: 'Program', body: [] }
```

The `.replit` file runs `npm install && npm start`, which won't work without a `package.json` — use the commands above instead.

## Scope

Learning exercise. It lays out the interfaces and control flow of a lexer/parser front-end without implementing the actual scanning or grammar logic. To make it real you'd fill in `tokenize` with a character scanner and `parse` with a recursive-descent grammar that builds actual AST nodes.
