# URL Shortener

A small Express API that maps long URLs to short numeric IDs. Based on the freeCodeCamp "URL Shortener Microservice" exercise.

## What it does

- `POST /api/shorturl` with a `url` form field. It validates the URL, checks the hostname resolves via DNS, then stores it and returns a short numeric id.
- `GET /api/shorturl/:short_url` redirects to the original URL for that id.

URLs are held in an in-memory array, so everything resets when the process restarts. Ids are a simple incrementing counter starting at 1.

## Stack

- Node.js
- Express
- body-parser (for URL-encoded form bodies)
- Node's built-in `dns` and `URL`

There is no `package.json` in this folder. Install the deps before running:

```bash
npm install express body-parser
node index.js
```

The server listens on port 3000.

## Usage

Create a short URL:

```bash
curl -X POST http://localhost:3000/api/shorturl \
  -d "url=https://www.google.com"
```

Response:

```json
{ "original_url": "https://www.google.com", "short_url": 1 }
```

Then visit `http://localhost:3000/api/shorturl/1` to be redirected to the original.

Bad input returns:

```json
{ "error": "invalid url" }
```

An unknown id returns:

```json
{ "error": "No short URL found" }
```

## Notes

- Validation is two-step: `new URL(url)` catches malformed strings, and `dns.lookup` on the hostname rejects domains that don't resolve.
- The URL must include a protocol (e.g. `https://`), otherwise `new URL` throws and you get the `invalid url` error.

## Scope

Practice project. In-memory storage, no persistence, no auth, no collision handling beyond a global counter. Fine for learning the request/response and validation flow, not meant for production.
