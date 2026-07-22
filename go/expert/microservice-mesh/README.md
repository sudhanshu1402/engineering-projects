# Microservice Mesh

A stub for a service mesh sidecar proxy in Go. Not implemented yet.

## Status

Scaffold only. `main.go` prints a line and leaves a `// Implement traffic interception` marker where the real work would go. There is no proxy, no traffic interception, no mesh logic here today.

```go
func main() {
    fmt.Println("Service Mesh Sidecar Proxy")
    // Implement traffic interception
}
```

## The idea

A service mesh moves cross-cutting network concerns (routing, retries, mTLS, observability) out of application code and into a sidecar proxy that sits next to each service and intercepts its traffic. This directory is the starting point for building that sidecar — currently just the entry point.

## Run

```sh
go run .
```

Prints `Service Mesh Sidecar Proxy` and exits. `go build` produces a binary that does the same.

No `go.mod` in this directory; it uses only the standard library (`fmt`).

## Scope

Placeholder for an expert-level Go exercise. Treat it as a TODO, not a working proxy.
