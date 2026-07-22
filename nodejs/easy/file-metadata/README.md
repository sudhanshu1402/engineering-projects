# File Metadata Microservice

A tiny Express service that accepts a file upload and returns its name, MIME type, and size in bytes. This is the freeCodeCamp "File Metadata Microservice" exercise.

## What it does

- `GET /` serves a bare HTML form with a file input.
- `POST /api/fileanalyse` takes a single uploaded file (form field `upfile`) and responds with JSON:

```json
{
  "name": "example.png",
  "type": "image/png",
  "size": 12345
}
```

If no file is attached, it returns `400 No file uploaded`.

## Stack

- Node.js + [Express](https://expressjs.com/)
- [multer](https://github.com/expressjs/multer) for multipart/form-data handling. Uploads are written to a local `uploads/` directory (multer's default disk storage); only the metadata is read back, the files themselves aren't served or cleaned up.

## Run

No `package.json` is checked in, so install the two deps first:

```bash
npm install express multer
node index.js
```

Server listens on port 3000. Open http://localhost:3000, pick a file, submit.

Or hit the endpoint directly:

```bash
curl -F "upfile=@/path/to/some/file.pdf" http://localhost:3000/api/fileanalyse
```

## Notes

- Size comes from `req.file.size` (actual bytes on disk), type from the browser-reported `mimetype` — so `type` reflects what the client claims, not content sniffing.
- No validation, size limits, or upload cleanup. It's a learning exercise, not production code.
- `.replit` runs `npm install && npm start`, but there's no `start` script defined here; run `node index.js` locally.
