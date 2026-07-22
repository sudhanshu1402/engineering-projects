# k8s-controller

Stub for a Kubernetes controller in Go. Not implemented yet.

## What this is

Right now `main.go` prints one line and exits:

```go
func main() {
    fmt.Println("Kubernetes Controller Stub")
    // Use k8s.io/client-go
}
```

That's the whole program. It's a placeholder for a real controller — the kind of process that watches Kubernetes resources and reconciles actual state toward desired state. The comment points at the intended dependency, `k8s.io/client-go`, but nothing uses it yet. There's no `go.mod`, no client, no reconcile loop.

## Run it

```bash
go run .
```

Prints:

```
Kubernetes Controller Stub
```

## Scope

Placeholder only. If you're looking for a working controller, this isn't one — it marks the spot where one would go.
