# web-server

A minimal TCP server in C that answers every request with the same `Hello world!` HTTP response.

## What it is

About 40 lines using the POSIX sockets API. It opens a `SOCK_STREAM` socket, binds to port 8080, listens, then loops forever accepting connections. For each connection it writes one hardcoded HTTP/1.1 response and closes the socket.

It does not parse the incoming request. It doesn't look at the method, path, or headers — anything you send gets the same reply. So it's not really a web server; it's a socket-programming exercise that happens to speak just enough HTTP for a browser to render one line.

## Build & run

The `.replit` file compiles it with:

```sh
gcc main.c -o main
./main
```

You'll see:

```
Server listening on port 8080
```

## Try it

With the server running:

```sh
curl http://localhost:8080
# Hello world!
```

Or open `http://localhost:8080` in a browser.

## Notes / rough edges

- The response uses `\n` line endings; HTTP wants `\r\n`. Most clients tolerate it, but it's technically malformed.
- `Content-Length: 12` is hardcoded and matches the 12-byte body ("Hello world!").
- Single-threaded and blocking — one connection is fully handled before the next is accepted. `listen(server_fd, 3)` sets a backlog of 3.
- No graceful shutdown; kill it with Ctrl-C.
- POSIX sockets, so Linux/macOS only.

Practice piece for learning the socket/bind/listen/accept flow, not production code.
