# PHP Projects

Small PHP practice scripts from college and early self-study, grouped by difficulty. Kept public as a learning archive.

> For active, production-grade work see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

## What's here

Each project is a single `index.php` file using plain PHP — sessions, superglobals (`$_POST`/`$_GET`/`$_SESSION`), server-side rendering with inline templates, and a bit of OOP in the harder ones. No framework, no Composer, no database. The difficulty labels track roughly how much each script attempts, not how polished it is: the `easy` and `medium` ones work end to end, while several `hard`/`expert` ones are deliberate stubs that sketch the shape of a bigger app.

## Projects

| Difficulty | Project | What it does |
|------------|---------|--------------|
| Easy | [contact-form](easy/contact-form) | Form that echoes a thank-you when name + email are filled, else an error. Escapes output with `htmlspecialchars`. |
| Easy | [simple-blog](easy/simple-blog) | Renders a hardcoded array of posts as a blog page with a `foreach` loop. |
| Medium | [task-list](medium/task-list) | Add-a-task form backed by `$_SESSION`; tasks persist for the session and render as a list. |
| Medium | [login-system](medium/login-system) | Session login with a hardcoded `admin`/`password` check, plus logout via query string. |
| Hard | [forum](hard/forum) | Stub: prints a fixed list of topics as links. Placeholder for a full forum. |
| Hard | [e-commerce](hard/e-commerce) | Stub: a `Product` class and a loop printing name + price. Placeholder for a shop. |
| Expert | [cms](expert/cms) | Stub: a `CMS` class with `renderPage($slug)` driven by `?page=`. Placeholder for a CMS. |
| Expert | [rest-api](expert/rest-api) | Returns a JSON status payload with the right `Content-Type` header. |

## Run any of them

Each needs a PHP runtime. Use the built-in server:

```bash
cd easy/contact-form        # or any project folder
php -S localhost:8000
```

Then open http://localhost:8000 in a browser. The `rest-api` one is easiest to check from the terminal:

```bash
cd expert/rest-api && php -S localhost:8000 &
curl http://localhost:8000
# {"status":"ok","message":"API working"}
```

## Scope note

These are learning exercises, not deployable apps. Credentials are hardcoded, state lives in sessions or arrays instead of a database, and the stub projects don't implement the behavior their names imply. That's the point of the archive: a record of early PHP work, warts and all.
