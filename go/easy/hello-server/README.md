# hello-server

A 15-line HTTP server in Go that replies "Hello, World!" to every request. A first-contact exercise with the standard library's `net/http`.

## What it does

Starts a server on port `8080` and registers one handler on `/`. Any request to any path returns the plain-text string `Hello, World!`, since `/` matches everything the default mux doesn't have a more specific route for.

## Stack

Standard library only (`net/http`, `fmt`). No `go.mod`, no third-party dependencies.

## Run

```sh
go run .
```

Then hit it:

```sh
curl http://localhost:8080/
# Hello, World!
```

To build a binary instead:

```sh
go build
./hello-server
```

## Notes

- Uses the default `ServeMux` via `http.HandleFunc` and passing `nil` to `ListenAndServe`.
- The return value of `http.ListenAndServe` is ignored, so a bind failure (e.g. port already in use) exits silently. Fine for a learning snippet; you'd want to check that error in real code.
- `.replit` runs `go run .` so it works on Replit out of the box.

## Scope

Practice piece. The point is the `net/http` boilerplate, nothing more.
