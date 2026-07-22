# Timestamp API

A tiny Express service that turns a date string or Unix timestamp into both formats. Clone of the freeCodeCamp "Timestamp Microservice" exercise.

## What it does

One route, `GET /api/:date?`, that returns a date as both a Unix millisecond timestamp and a UTC string.

- No `:date` given -> returns the current time.
- `:date` that's all digits -> treated as a Unix timestamp (milliseconds) and parsed with `new Date(parseInt(date))`.
- Anything else -> passed straight to `new Date(date)`, so any string JavaScript's `Date` understands works (e.g. `2015-12-25`).
- Unparseable input -> `{ "error": "Invalid Date" }`.

## Stack

- Node.js
- Express

There's no `package.json` in this folder, so `npm install` won't pull Express in on its own. Install it first:

```bash
npm init -y
npm install express
node index.js
```

The server listens on port 3000.

## Usage

```bash
# current time
curl http://localhost:3000/api
# {"unix":1690000000000,"utc":"Sat, 22 Jul 2026 00:00:00 GMT"}

# a date string
curl http://localhost:3000/api/2015-12-25
# {"unix":1451001600000,"utc":"Fri, 25 Dec 2015 00:00:00 GMT"}

# a unix timestamp (ms)
curl http://localhost:3000/api/1451001600000
# {"unix":1451001600000,"utc":"Fri, 25 Dec 2015 00:00:00 GMT"}

# garbage
curl http://localhost:3000/api/not-a-date
# {"error":"Invalid Date"}
```

## Notes

- The digit check uses `!isNaN(date)`, so any purely numeric string is read as a Unix timestamp rather than a date. `1451001600000` is treated as ms since epoch, not the year.
- Timestamps are in milliseconds, matching JavaScript's `Date.getTime()`.
- `.replit` runs `npm install && npm start`, but there's no `start` script defined here — run `node index.js` locally.

Learning exercise, kept deliberately small.
