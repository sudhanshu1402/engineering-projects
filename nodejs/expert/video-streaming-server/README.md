# Video Streaming Server

A ~35-line Express server that streams an MP4 over HTTP with byte-range support, so a browser `<video>` tag can seek and buffer instead of downloading the whole file.

## What it does

One route, `GET /video`, serves `sample.mp4`:

- If the request has a `Range` header (what browsers send when you scrub the timeline), it parses `start`/`end`, opens a read stream for just that slice, and replies `206 Partial Content` with `Content-Range`, `Accept-Ranges`, and `Content-Length` for the chunk.
- If there's no `Range` header, it replies `200 OK` and pipes the whole file.

That range handling is the whole point of the exercise — it's what makes video seekable and lets the browser fetch progressively rather than in one shot.

## Stack

- Node.js
- Express (only dependency)
- Node's built-in `fs` for `statSync` and `createReadStream`

There's no `package.json` in this folder. Install Express before running:

```bash
npm init -y
npm install express
```

## Run

You also need a file named `sample.mp4` in this directory — `fs.statSync('sample.mp4')` will throw on startup request if it's missing. Drop any MP4 in and rename it.

```bash
node index.js
```

Server listens on port 3000.

## Usage

Point a browser or video element at the route:

```html
<video controls src="http://localhost:3000/video"></video>
```

Or check the range behavior directly with curl:

```bash
# whole file -> 200
curl -I http://localhost:3000/video

# first 1 KB -> 206 Partial Content
curl -H "Range: bytes=0-1023" -i http://localhost:3000/video
```

## Notes / scope

This is a learning exercise, kept deliberately minimal:

- The file path and content type are hardcoded to `sample.mp4` / `video/mp4`.
- No validation on the `Range` values — a malformed or out-of-bounds range isn't rejected.
- `statSync` runs on every request (blocking) rather than being cached.
- No error handling if the file is missing, no auth, no config.

It's meant to show how HTTP range requests power video seeking, not to be a production server.
