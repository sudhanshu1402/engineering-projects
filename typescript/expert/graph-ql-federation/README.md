# GraphQL Federation

A minimal Apollo Federation gateway that stitches two subgraphs into one GraphQL API.

## What this is

A single file, `gateway.ts`, that spins up an `ApolloGateway` pointed at two subgraph services — `accounts` on port 4001 and `reviews` on port 4002 — and serves the composed supergraph through an `ApolloServer`. It's a learning snippet showing the shape of a federated setup, not a full running system.

```ts
const gateway = new ApolloGateway({
    serviceList: [
        { name: 'accounts', url: 'http://localhost:4001' },
        { name: 'reviews', url: 'http://localhost:4002' }
    ]
});
```

The gateway queries each subgraph's SDL, composes them into a single schema, and routes incoming queries to the right service. Clients hit one endpoint and can query across both domains in a single request.

## Scope note

This is only the gateway. The `accounts` and `reviews` subgraph servers it points at aren't part of this directory — you'd need to run federated subgraphs on 4001 and 4002 for the gateway to compose a schema. On its own it demonstrates the gateway wiring; it won't serve queries without those upstreams live.

Also note the code uses `serviceList` with `apollo-server`, the older Apollo Gateway/Server API. Newer Apollo (`@apollo/server` v4, gateway with managed federation or `IntrospectAndCompose`) has moved on from this pattern.

## Stack

- `@apollo/gateway` — composes subgraph schemas into a supergraph
- `apollo-server` — serves the composed schema
- TypeScript

## Run

There's no `package.json` checked in here. To run it standalone:

```bash
npm init -y
npm install @apollo/gateway apollo-server graphql
npx ts-node gateway.ts
```

The `.replit` file runs `npm install && npm start`, so on Replit you'd add a `start` script (e.g. `ts-node gateway.ts`) to `package.json`.

Once running, the gateway prints its URL:

```
Gateway ready at http://localhost:4000/
```

With both subgraphs up, you can query fields from `accounts` and `reviews` together against that single endpoint.
