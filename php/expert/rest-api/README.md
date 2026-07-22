# rest-api

A one-file PHP script that returns a JSON health-check response. This is a minimal practice snippet, not a real REST API.

## What it does

`index.php` sets a JSON content-type header and echoes a fixed payload:

```json
{"status":"ok","message":"API working"}
```

That's the whole thing. There's no routing, no HTTP methods, no data store, and no framework. Despite the folder path (`expert`) and the old README's mention of Laravel, none of that is present — it's plain PHP.

## Run it

You need PHP installed. From this directory, start the built-in server:

```bash
php -S localhost:8000
```

Then hit it:

```bash
curl http://localhost:8000/index.php
# {"status":"ok","message":"API working"}
```

Or run the file directly to see the raw output:

```bash
php index.php
```

## Scope

Learning snippet. It demonstrates setting a JSON header and using `json_encode` to return a response — the very first step toward building an API, and nothing beyond that. To make it an actual REST API you'd add request routing, HTTP verb handling, and real data.
