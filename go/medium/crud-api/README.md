# crud-api

A minimal in-memory HTTP store in Go. One file, standard library only.

## What it is

A practice exercise: a single `/items` endpoint backed by a `map[string]Item` guarded by a `sync.RWMutex`. It listens on port `8080` and keeps everything in memory, so data is gone when the process exits.

Despite the name, it isn't full CRUD yet — only two operations are wired up:

- `GET /items` — returns every stored item as a JSON array.
- `POST /items` — decodes a JSON `{"id": "...", "name": "..."}` body and upserts it into the map keyed by `id`.

There's no update-by-id or delete endpoint, and POST returns no body or status on success. It's a learning cut, not a finished service.

## The item shape

```go
type Item struct {
    ID   string `json:"id"`
    Name string `json:"name"`
}
```

## Run

Only the Go standard library is used — no `go.mod`, no external dependencies.

```sh
go run .
```

## Try it

```sh
# add an item
curl -X POST localhost:8080/items -d '{"id":"1","name":"widget"}'

# list all items
curl localhost:8080/items
# [{"id":"1","name":"widget"}]

# posting the same id overwrites it
curl -X POST localhost:8080/items -d '{"id":"1","name":"gadget"}'
curl localhost:8080/items
# [{"id":"1","name":"gadget"}]
```

## Notes

- The store is a struct that embeds `sync.RWMutex`: reads take `RLock`, writes take `Lock`. That's the one detail worth taking from this — concurrent-safe map access done the plain way.
- A malformed POST body is silently ignored (the decode error is dropped and nothing is stored).
- GET output isn't ordered — map iteration order is random.
