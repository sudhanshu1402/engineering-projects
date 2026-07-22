# Simple Blog

A single-file PHP page that loops over a hardcoded array of posts and prints them as HTML. A beginner exercise in mixing PHP with HTML markup.

## What it does

`index.php` defines two blog posts in a PHP array, then uses a `foreach` loop with alternative syntax (`foreach ... endforeach`) to render each one's title and content inside the page. That's the whole thing — no database, no routing, no framework.

It's here to practice two basics:
- Embedding PHP inside HTML and escaping in/out of `<?php ?>` tags.
- The short echo tag `<?= ... ?>` for printing values.

## Stack

Plain PHP. No dependencies, no build step, no framework. (Despite the folder path, there's no Laravel here.)

## Run it

You need PHP installed. From this directory:

```bash
php -S localhost:8000
```

Then open http://localhost:8000 in a browser.

Or run it straight through the CLI to see the raw HTML output:

```bash
php index.php
```

## The data

Posts are hardcoded near the top of the file:

```php
$posts = [
    ["title" => "First Post", "content" => "Hello World!"],
    ["title" => "PHP is cool", "content" => "It is widely used."]
];
```

To change what shows up, edit that array. Each entry needs a `title` and a `content` key.

## Scope

Learning toy, not a real blog. Posts are static, there's no way to add or edit them at runtime, and output isn't HTML-escaped (fine for this fixed data, not fine for user input). Next steps if you wanted to grow it: read posts from a file or database, add a form to create them, and escape output with `htmlspecialchars`.
