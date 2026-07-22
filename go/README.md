# Go Projects

> Part of my public learning archive. For active, production-grade work see the pinned repos on my [GitHub profile](https://github.com/sudhanshu1402).

Go practice code from college and self-study, sorted by difficulty. The focus was the standard library, concurrency (goroutines, `sync`, `sync/atomic`), and the basics of systems and network programming. It ranges from finished small programs to design stubs I used to sketch out harder projects.

## How it's organized

Four folders by difficulty: `easy/`, `medium/`, `hard/`, `expert/`. Each project lives in its own folder with a `main.go`.

Some entries are complete programs; others are deliberate stubs — a single `main.go` that prints a line and a comment naming the library or algorithm the real build would use. The status column below is honest about which is which.

## Projects

| Difficulty | Project | What it is | Status |
|---|---|---|---|
| Easy | [number-guess](easy/number-guess) | CLI game: guess a random 1–100 number, prints Higher/Lower until you win | Complete |
| Easy | [hello-server](easy/hello-server) | Minimal `net/http` server returning "Hello, World!" on `:8080` | Complete |
| Medium | [crud-api](medium/crud-api) | In-memory REST API for items; `GET`/`POST /items`, guarded by a `sync.RWMutex` | Complete |
| Medium | [slack-bot](medium/slack-bot) | Stub — prints a placeholder; real version would use `github.com/slack-go/slack` | Stub |
| Hard | [load-balancer](hard/load-balancer) | Round-robin HTTP load balancer over 3 backends, atomic peer selection, background health-check goroutine, unit tests | Complete |
| Hard | [distributed-cache](hard/distributed-cache) | Stub — placeholder for a consistent-hashing cache node | Stub |
| Expert | [k8s-controller](expert/k8s-controller) | Stub — placeholder for a `client-go` Kubernetes controller | Stub |
| Expert | [microservice-mesh](expert/microservice-mesh) | Stub — placeholder for a sidecar proxy with traffic interception | Stub |

## Running

Most projects are a single file with no dependencies:

```bash
cd easy/number-guess
go run main.go
```

The load balancer has its own module and tests:

```bash
cd hard/load-balancer
go run main.go        # starts the balancer on :8000
go test ./...         # runs the ServerPool / ServerNode tests
```

## Worth a look

- **load-balancer** is the most complete piece. `ServerPool.GetNextPeer` walks the backend ring with an atomic counter and skips dead nodes; a goroutine re-checks health every 10s. Forwarding uses a plain `http.Get` — the code comments flag that production would use `httputil.ReverseProxy`. Backends and the health check are mocked, so it runs standalone.
- **crud-api** shows the standard-library approach to a concurrent-safe store: an anonymous struct embedding `sync.RWMutex` around a `map[string]Item`, read-locked for lists and write-locked for inserts.

## Scope

A learning archive, not a library. The stub projects are starting points I never finished, kept here for transparency about where each idea stopped. The finished ones are small by design.
