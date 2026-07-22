# Express TS API

A minimal Express server in TypeScript with one typed route. Practice piece for wiring up Express with TypeScript types.

## What it does

Starts an HTTP server on port 3000 with a single endpoint:

- `GET /user/:id` — returns a JSON `User` object. The `id` comes from the URL, the name is hardcoded (`"John Doe"`).

The point of the exercise is the typing: `Request`/`Response` are typed from Express, and the response is shaped by a local `User` interface (`{ id: number; name: string }`).

## Stack

- TypeScript
- Express

There's no `package.json` checked in, so install both directly.

## Run

```bash
npm install express
npm install -D typescript @types/express @types/node ts-node

# run without compiling
npx ts-node server.ts
```

Or compile and run:

```bash
npx tsc server.ts
node server.js
```

Server logs `TS API running` when it's up.

## Example

```bash
curl http://localhost:3000/user/42
# {"id":42,"name":"John Doe"}
```

`req.params.id` is a string, so it's run through `parseInt` before going into the `User.id` number field.

## Scope

Toy example — a single stub route with no persistence, validation, or error handling. It's here to demonstrate Express + TypeScript setup, not to be a real API.
