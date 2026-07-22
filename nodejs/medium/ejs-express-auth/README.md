# EJS Express Auth

Placeholder for a server-rendered authentication app built with Express and EJS templates. **Not implemented yet** — this directory currently holds only this README.

## Status

Empty scaffold. There is no `package.json`, no source files, and no `views/` directory despite what an earlier auto-generated README claimed. Nothing here runs.

## Intended scope

The name points at a classic learning exercise: username/password auth with server-side rendered pages.

- Express as the web server
- EJS for server-rendered login / signup / dashboard pages
- Session or JWT-based login state
- Password hashing (e.g. bcrypt)

None of that exists in code yet. Treat the list above as the plan, not a feature set.

## If you're picking this up

Start from scratch:

```bash
npm init -y
npm install express ejs express-session bcrypt
```

Then add an `app.js` entry point and a `views/` folder for the EJS templates.
