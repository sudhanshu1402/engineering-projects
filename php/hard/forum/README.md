# Forum

A stub. Prints a hardcoded list of two forum topics as HTML links.

## What it actually is

`index.php` is 8 lines. It defines an array of two topic names (`General Discussion`, `Help & Support`) and echoes each one inside a `<div>` with a dead `#` link. That's the whole program. No routing, no database, no posts, no users.

Despite living under `hard/`, this is a placeholder, not a working forum.

## Run it

Needs PHP. From this directory:

```bash
php -S localhost:8000
```

Then open http://localhost:8000 in a browser. Or just run `php index.php` to dump the raw HTML to your terminal.

## Output

```html
<h1>Forum Stub</h1>
<div><a href='#'>General Discussion</a></div>
<div><a href='#'>Help & Support</a></div>
```

## Scope

Placeholder only. To become a real forum it would need at minimum: persistent storage for topics and posts, a way to create threads and replies, and real links instead of `#`.
