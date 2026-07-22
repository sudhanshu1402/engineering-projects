# Login System

A single-file PHP login demo using PHP sessions. Practice exercise, not production code.

## What it does

`index.php` shows a login form. Submit the username `admin` and password `password` and it stores `admin` in `$_SESSION`. While that session key is set, the page shows "Welcome Admin!" with a logout link. Hitting `?logout` destroys the session and redirects back to the form.

That's the whole app. The point is to show how PHP sessions gate a page: set a session value on login, check it on each request, clear it on logout.

## Stack

Plain PHP with the built-in `$_SESSION`, `$_POST`, and `$_GET` superglobals. No framework, no database, no Composer. (The old README said Laravel — it isn't.)

## Run

Use the PHP built-in server from this directory:

```bash
php -S localhost:8000
```

Then open http://localhost:8000 in a browser. Log in with:

- User: `admin`
- Pass: `password`

Click **Logout** (or visit `?logout`) to end the session.

## Notes on the code

- Credentials are hardcoded in the source (`index.php`, lines 4). There is no user store.
- The credential check uses `==` (loose comparison) rather than `===`.
- The password is compared in plaintext — no hashing.
- No CSRF token on the form.
- `header("Location: ...")` on logout runs after some conditional output has already been decided, but since nothing is echoed before it on the logout path, the redirect works.

These are fine for a learning demo and would all need fixing before anything real. It exists to practice the session login/logout cycle, nothing more.
