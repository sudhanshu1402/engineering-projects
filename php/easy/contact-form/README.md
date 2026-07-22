# Contact Form

A single-file PHP script: an HTML form that posts back to itself and prints a greeting when name and email are filled in.

This is a beginner practice exercise. It covers the basics of handling a form submission in plain PHP: reading `$_POST`, validating that fields aren't empty, and escaping output.

## What it does

- Renders a form with `name` and `email` text inputs and a submit button.
- On submit, the page posts to itself (`method="post"`, no action attribute).
- If both `name` and `email` are non-empty, it echoes `Thanks, <name>`.
- If either is missing, it echoes `Please fill all fields.`
- The submitted name is passed through `htmlspecialchars()` before printing, so `<script>` and other HTML in the input is escaped rather than rendered.

## Stack

Plain PHP. No framework, no dependencies, no build step. One file: `index.php`.

(Note: the folder lives under a `php/easy` path, but there is no Laravel here despite what an earlier README claimed — it's raw PHP.)

## Run it

You need PHP installed. From this directory:

```bash
php -S localhost:8000
```

Then open http://localhost:8000 in a browser. Or drop `index.php` into any Apache/Nginx+PHP webroot.

## Example

Enter `Ada` in Name and `ada@example.com` in Email, submit, and the page shows:

```
Thanks, Ada
```

Leave either field blank and it shows:

```
Please fill all fields.
```

## Scope

Toy exercise, not production code. Things a real contact form would add and this doesn't: proper email format validation, CSRF protection, sending the message anywhere (email/DB), and styling. The email field also isn't `type="email"`, so the browser won't validate it.
