# Blog API

A minimal CRUD REST API for blog posts, built with Express. One file, in-memory storage. A practice piece for wiring up the four HTTP verbs against a resource.

## What it does

Exposes a `/posts` resource with create, read, update, and delete. Posts live in a plain array in memory, keyed by an auto-incrementing integer id. There's no database, auth, or persistence — restart the process and the data is gone.

The "hard" folder label overstates it; this is a straightforward Express router exercise.

## Stack

- Node.js
- Express (the only dependency)

No `package.json` is checked in, so install Express before running:

```bash
npm install express
node index.js
```

The server listens on port 3000.

(The `.replit` file runs `npm install && npm start`, which assumes a `package.json` with a `start` script — neither exists in the repo, so use `node index.js` locally.)

## Endpoints

| Method | Path         | Body                | Response |
|--------|--------------|---------------------|----------|
| POST   | `/posts`     | `{ title, content }`| `201` + created post |
| GET    | `/posts`     | —                   | `200` + array of all posts |
| GET    | `/posts/:id` | —                   | `200` + post, or `404` |
| PUT    | `/posts/:id` | `{ title, content }`| `200` + updated post, or `404` |
| DELETE | `/posts/:id` | —                   | `204` |

## Example

```bash
# create
curl -X POST http://localhost:3000/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"First","content":"Hello world"}'
# -> {"id":1,"title":"First","content":"Hello world"}

# list
curl http://localhost:3000/posts

# fetch one
curl http://localhost:3000/posts/1

# update
curl -X PUT http://localhost:3000/posts/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Edited","content":"Updated body"}'

# delete
curl -X DELETE http://localhost:3000/posts/1
```

## Scope notes

Deliberately bare. Known gaps if you wanted to take it further:

- No input validation — POST/PUT accept whatever's in the body, so `title`/`content` can be `undefined`.
- DELETE always returns `204`, even for an id that doesn't exist.
- State is an in-process array; not safe across restarts or multiple instances.
