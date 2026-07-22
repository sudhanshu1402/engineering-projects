# Load Balancer

A round-robin HTTP load balancer in Go. Listens on one port, forwards each request to the next healthy backend in the pool.

## What it does

Runs an HTTP server on `:8000`. Every incoming request is routed to a backend picked by round-robin. The picker skips backends marked dead, so if a server is down it moves on to the next live one. If no backend is alive, it returns `503 Service Unavailable`.

Backends are hardcoded to three local addresses:

```
http://localhost:8081
http://localhost:8082
http://localhost:8083
```

A background goroutine loops every 10 seconds as a health-check slot. Right now it's a stub that marks every backend alive — the real probe isn't implemented.

This is a learning exercise, not a production proxy. See the scope notes below.

## Stack

- Go 1.20, standard library only (`net/http`, `net/url`, `sync/atomic`). No external dependencies.

## Build & run

```bash
go run .
# or
go build && ./load-balancer
```

Then hit the balancer:

```bash
curl http://localhost:8000/
```

You'll get a `502 Backend Error` unless something is actually listening on 8081-8083 — the balancer only forwards, it doesn't start backends. To see it work, run throwaway servers on those ports first, e.g.:

```bash
python3 -m http.server 8081 &
python3 -m http.server 8082 &
python3 -m http.server 8083 &
```

The console prints which backend each request was sent to (`Redirecting to http://localhost:8081`).

## Tests

```bash
go test .
```

Covers three units: adding a backend to the pool, round-robin index advancing, and the alive/dead flag toggling.

## How the round-robin works

`NextIndex()` uses `atomic.AddUint64` on a shared counter, so peer selection is safe under concurrent requests without a mutex on the counter itself. `GetNextPeer()` starts at that index and walks a full cycle looking for a live backend; when it has to skip past dead ones it stores the landed index back so the next call resumes from there. The per-backend alive flag is guarded by a `sync.RWMutex`.

## Scope / known gaps

Honest about what this is — a practice implementation of the load-balancing loop, not a drop-in proxy:

- **Not a real reverse proxy.** `lbHandler` uses `http.Get(peer.URL)`, which discards the request method, path, headers, and body — every request becomes a plain GET to the backend root. The code comments say to use `httputil.ReverseProxy` in production; it isn't wired up here.
- **Health check is a stub.** The 10-second loop marks every backend alive unconditionally, so dead-backend skipping only triggers if you call `SetAlive(false)` yourself (as the test does).
- **Backends are hardcoded** in `main.go`, no config file or flags.
- **`ServerNode.ReverseProxy` field is declared but unused.**
