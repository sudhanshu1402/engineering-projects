# TypeScript Projects

> Part of my public learning archive. For active, production-grade work see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

A set of small TypeScript exercises I wrote while learning the language and its ecosystem. They start with plain functions and build up to framework and tooling patterns (Express, React, NestJS, Next.js, Apollo Federation, a toy compiler front end). Most files are deliberately short — they demonstrate one idea each, not finished applications.

## Layout

Projects are grouped into four difficulty tiers. Each project lives in its own folder with an `index`/entry file and a short README.

```
typescript/
├── easy/
│   ├── ts-calculator/
│   └── ts-to-do-cli/
├── medium/
│   ├── express-ts-api/
│   └── react-ts-widget/
├── hard/
│   ├── nest-js-blog/
│   └── next-js-ecommerce/
└── expert/
    ├── compiler-transpiler/
    └── graph-ql-federation/
```

## Projects

| Tier | Project | What it shows |
|------|---------|---------------|
| easy | [ts-calculator](easy/ts-calculator) | A typed `calculate(a, b, op)` function using a `switch` over the operator. |
| easy | [ts-to-do-cli](easy/ts-to-do-cli) | Interactive terminal to-do list built on Node's `readline` (`add`/`list`/`exit`). |
| medium | [express-ts-api](medium/express-ts-api) | Express server with a typed `GET /user/:id` route returning a `User` interface. |
| medium | [react-ts-widget](medium/react-ts-widget) | A typed `React.FC` counter component with `useState<number>` and a `Props` interface. |
| hard | [nest-js-blog](hard/nest-js-blog) | Minimal NestJS app: a decorated `@Controller`/`@Module` with a single `@Get` route. |
| hard | [next-js-ecommerce](hard/next-js-ecommerce) | Next.js page using `getStaticProps` to render a typed list of products. |
| expert | [compiler-transpiler](expert/compiler-transpiler) | Skeleton of a compiler front end: `tokenize` → `parse` producing an AST-shaped object. |
| expert | [graph-ql-federation](expert/graph-ql-federation) | Apollo Gateway stitching two subgraphs (`accounts`, `reviews`) behind one server. |

## Stack

- **Language:** TypeScript 5.2 (`strict` mode, `experimentalDecorators` + `emitDecoratorMetadata` on for the NestJS example)
- **Target/module:** ES2016 / CommonJS
- **Frameworks used across the tiers:** Express, React 18, NestJS 10, Next.js 13, Apollo Gateway / Apollo Server

Dependencies and the compiler config are shared from the root `package.json` and `tsconfig.json`.

## Build & run

Install once from this directory, then compile:

```bash
npm install
npm run build   # runs tsc
```

Run an individual exercise with a TypeScript runner, for example:

```bash
npx ts-node easy/ts-calculator/index.ts
npx ts-node easy/ts-to-do-cli/index.ts
```

The server and framework examples (`express-ts-api`, `nest-js-blog`, `graph-ql-federation`) listen on their own ports once started; `next-js-ecommerce` is a Next.js page and expects a Next dev server. Each folder also carries a `.replit` file, so the projects can be opened and run directly on Replit.

## Example

`easy/ts-calculator/index.ts`:

```ts
function calculate(a: number, b: number, op: string): number {
    switch (op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return a / b;
        default: return 0;
    }
}
console.log("5 + 3 =", calculate(5, 3, '+'));  // 5 + 3 = 8
```

## Scope

These are learning stubs, not products. The harder-tier examples (compiler, GraphQL federation, the framework apps) are intentionally minimal — enough to show the shape of the pattern and get the types right, not to be complete or deployable. Kept public for transparency about how I learned the language.
