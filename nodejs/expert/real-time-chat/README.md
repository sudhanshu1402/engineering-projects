# Real-Time Chat

A minimal broadcast chat server built with Express and Socket.IO. One room, no auth, no persistence — every message a client sends is echoed to everyone connected.

## What it does

`server.js` starts an HTTP server on port 3000. On the WebSocket side it listens for `chat message` events and re-emits them to all connected sockets with `io.emit`, so the whole room sees each message in real time. The root route (`/`) serves an `index.html` from the same directory.

This is a learning exercise — essentially the canonical Socket.IO "hello world" chat, kept deliberately small.

## Stack

- Node.js
- [Express](https://expressjs.com/) — HTTP server and static file serving
- [Socket.IO](https://socket.io/) — WebSocket transport and event handling

## Run

```bash
npm install express socket.io
node server.js
```

Then open http://localhost:3000.

## Heads up — incomplete as committed

The code won't run as-is without two missing pieces:

- **No `index.html`.** `server.js` does `res.sendFile(__dirname + '/index.html')`, but that file isn't in this directory. You need a client page that loads `/socket.io/socket.io.js`, emits `chat message` on submit, and renders incoming `chat message` events. Without it, `/` returns an error.
- **No `package.json`.** So `npm install` has nothing to read and `npm start` has no script. Install the deps by name (above), or add a `package.json` first. The `.replit` file expects `npm install && npm start` to work.

The old README also pointed at `node index.js`; the actual entry file is `server.js`.

## How it works

```js
io.on('connection', (socket) => {
    socket.on('chat message', (msg) => {
        io.emit('chat message', msg);   // broadcast to everyone, sender included
    });
});
```

- `io.emit` broadcasts to all clients. Use `socket.broadcast.emit` instead if you don't want to echo back to the sender.
- No rooms, usernames, history, or input sanitization. Messages live only for the moment they're broadcast.

## Scope

Practice project. To make it real you'd add the client page, a `package.json`, and probably usernames, rooms, and message persistence.
