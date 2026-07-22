# nest-js-blog

A single-file NestJS starter: one controller, one route. Named "blog" but the only endpoint returns cats.

## What it is

A minimal NestJS bootstrap in one file (`main.ts`). It wires up:

- `CatsController` with a `GET /cats` route that returns the string `This action returns all cats`
- `AppModule` registering that controller
- a `bootstrap()` call that starts the HTTP server on port 3000

That's the whole thing. It's a practice piece for learning how NestJS decorators (`@Controller`, `@Get`, `@Module`) and `NestFactory.create` fit together, kept in one file instead of the usual multi-file NestJS layout.

## Stack

- TypeScript
- `@nestjs/core`, `@nestjs/common`

Note: there's no `package.json` or `tsconfig.json` in this directory, so dependencies aren't pinned here. The `.replit` file runs `npm install && npm start`, which assumes a `package.json` with those deps and a `start` script exists at runtime (Replit's environment).

## Run

On Replit the configured command is:

```
npm install && npm start
```

To run locally you'd need to add a `package.json` (with `@nestjs/core`, `@nestjs/common`, `reflect-metadata`, `rxjs`) and a `tsconfig.json` with decorator support (`experimentalDecorators` and `emitDecoratorMetadata` on), then:

```
npm install
npx ts-node main.ts
```

## Try it

Once running:

```
curl http://localhost:3000/cats
# This action returns all cats
```

## Scope

Toy / learning exercise. One route, no database, no blog. It's here to show the NestJS request-handling skeleton, nothing more.
