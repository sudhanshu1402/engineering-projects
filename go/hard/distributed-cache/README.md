# Distributed Cache

A Go scaffold for a distributed cache node. Not implemented yet — right now it's a stub.

## Status

Early scaffold. `main.go` prints a startup line and has a `// Implement consistent hashing here` marker. There's no cache, no networking, no hashing logic yet.

```go
func main() {
    fmt.Println("Distributed Cache Node Started")
    // Implement consistent hashing here
}
```

## Intended direction

The placeholder points at consistent hashing — the usual approach for a distributed cache: hash keys and nodes onto a ring so keys map to nodes, and adding or removing a node only reshuffles a small slice of keys instead of everything. None of that exists in the code today; it's the plan the comment hints at.

## Run

```bash
go run .
```

Prints:

```
Distributed Cache Node Started
```

`go build` compiles a binary. No dependencies — standard library only, no `go.mod` in the directory.

## Scope

Practice project under `go/hard`. Placeholder committed as a starting point; the real work (ring, node membership, key distribution, a get/set API) is still to be written.
