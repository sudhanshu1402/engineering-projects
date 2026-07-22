# CMS

A single-file PHP stub that echoes back a page slug from the query string. Named "CMS," but it's a starting skeleton, not a content management system.

## What it does

`index.php` defines one class, `CMS`, with a single method `renderPage($slug)` that HTML-escapes the slug and prints `Rendering page for: <slug>`. The script reads `?page=` from the URL (defaulting to `home`) and calls it.

That's the whole thing:

```php
class CMS
{
    public function renderPage($slug)
    {
        echo "Rendering page for: " . htmlspecialchars($slug);
    }
}

$cms = new CMS();
$cms->renderPage(isset($_GET['page']) ? $_GET['page'] : 'home');
```

No templates, routing, database, or storage. `htmlspecialchars` on the slug is the one real touch — it stops the echoed input from being an XSS vector.

## Stack

Plain PHP. No framework, no Composer, no dependencies. (The old README claimed Laravel; there's no Laravel here.)

## Run

Serve the directory with PHP's built-in server:

```bash
php -S localhost:8000
```

Then:

```
http://localhost:8000/index.php            -> Rendering page for: home
http://localhost:8000/index.php?page=about -> Rendering page for: about
```

Or run it straight from the CLI:

```bash
php index.php
# Rendering page for: home
```

## Scope

Practice stub. The `renderPage` method is the seed you'd build a real page loader around — swap the `echo` for template lookup and content fetching. As it stands it does exactly the two things above.
