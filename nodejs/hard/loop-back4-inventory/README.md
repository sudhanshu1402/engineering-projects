# LoopBack 4 Inventory

Planned inventory service built on the LoopBack 4 framework. Not yet implemented — this directory is currently a placeholder.

## Status

There is no code here yet. The only file is this README. Nothing to build or run.

The name points at the intended shape of the project: a REST API for tracking inventory (items, stock levels, maybe suppliers/orders) using [LoopBack 4](https://loopback.io/), IBM's TypeScript/Node.js API framework. LoopBack 4 leans on decorators for models, repositories, and controllers, and generates an OpenAPI spec and Swagger UI out of the box.

## What it would take to start

LoopBack 4 projects are scaffolded with the official CLI, not by hand:

```bash
npm install -g @loopback/cli
lb4 app loop-back4-inventory
cd loop-back4-inventory
lb4 model Item
lb4 datasource db
lb4 repository
lb4 controller Item
npm start
```

That gives you the standard layout (`src/models`, `src/repositories`, `src/controllers`, `src/datasources`) and a running server with Swagger UI at `http://localhost:3000/explorer`.

## Scope

Filed under `nodejs/hard` as a learning exercise. Treat this README as a stub until real source lands — none of the above has been written yet.
