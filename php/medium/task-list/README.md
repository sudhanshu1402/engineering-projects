# Task List

A one-file PHP script that adds tasks to a list and shows them. Practice exercise for PHP sessions and form handling.

## What it does

Type a task, hit Add, and it appends to a list rendered below the form. The list lives in `$_SESSION`, so it survives page reloads for as long as your session cookie lasts. There's no database and no file storage — restart the session (or clear cookies) and the list is gone.

## Stack

Plain PHP. No framework, no dependencies, no Composer. Runs on any PHP interpreter with sessions enabled.

## Run it

From this directory:

```bash
php -S localhost:8000
```

Then open http://localhost:8000/index.php and add tasks.

## How it works

The whole thing is `index.php` (19 lines):

- `session_start()` on every request, initializing `$_SESSION['tasks']` to an empty array the first time.
- A POST with a `task` field gets appended to that array.
- The array is looped and each item printed inside `<li>` tags, escaped with `htmlspecialchars()` so task text can't inject HTML.

## Scope

Toy project. No editing or deleting tasks, no persistence beyond the session, no validation (an empty submit adds a blank entry). It's here to demonstrate the session + POST loop, not to be a real app.
