# Library Management System

A Flask + MySQL web app for running a small lending library: catalog books, register members, issue and return copies, track rental fees and debt, and pull a couple of reports. Built as a dev hiring test.

## What it does

The app models the day-to-day of a paid lending library:

- **Books** — full CRUD, plus fields for ISBN/ISBN13, rating, page count, publisher, publication date, and stock counts (`total_quantity`, `available_quantity`, `rented_count`).
- **Members** — add, edit, delete, and view. Each member carries an `outstanding_debt` and `amount_spent`.
- **Issue a book** — creates a transaction, decrements `available_quantity`, bumps `rented_count`. Refuses to issue if no copies are free.
- **Return a book** — charges `per_day_fee × days held`, records how much the member actually paid, and rolls the shortfall into their outstanding debt. A member is blocked from returning if it would push their debt past Rs. 500.
- **Import books** — pulls records from the public Frappe library API (`frappe.io/api/method/frappe-library`) by title/author/ISBN/publisher, skipping any book IDs already in the DB, and reports how many it actually imported.
- **Search** — books by title or author (SQL `LIKE`).
- **Reports** — top 5 members by spend, top 5 books by rental count.

### Business rules worth noting

- When a book is added, `available_quantity` is initialized to `total_quantity`.
- Editing a book's total stock adjusts availability by the delta (`available += new_total − old_total`), so already-issued copies aren't lost.
- Return charge is whole-days only (`(now − borrowed_on).days`), so a same-day return costs nothing.
- Delete is wrapped in a try/except — deleting a book or member still referenced by a transaction hits a foreign-key constraint and flashes an error instead of crashing.

## Stack

- **Flask** — routing and templating (Jinja2)
- **Flask-MySQLdb** (`MySQLdb`) — DB access from the app, with `DictCursor` so rows come back as dicts
- **WTForms** — form definitions and validation
- **mysql-connector-python** — used only by the DB setup script and test setup
- **requests** — Frappe API import

Front end is server-rendered templates under `dev-hiring-test/templates/` extending a shared `layout.html`.

## Database

Three tables (`dev-hiring-test/library-db.sql`):

- `books` — catalog + stock counts
- `members` — profile + `outstanding_debt`, `amount_spent`
- `transactions` — one row per issue/return, FK to `books` and `members`, with `borrowed_on`, `returned_on`, `total_charge`, `amount_paid`

A parallel `librarytestdb` schema (`library-test-db.sql`) exists for the test suite.

## Configuration

The app reads MySQL settings from environment variables, falling back to local defaults:

| Var | Default |
|---|---|
| `MYSQL_HOST` | `localhost` |
| `MYSQL_USER` | `root` |
| `MYSQL_PASSWORD` | `` (empty) |
| `MYSQL_PORT` | `3306` |
| `MYSQL_DB` | `librarydb` |

## Build & run

From `dev-hiring-test/`:

```bash
pip install -r requirements.txt

# create both databases + tables (needs a running MySQL)
python setup_db.py

# start the app
python app.py
```

The app serves on Flask's default `http://127.0.0.1:5000` with `debug=True`.

## Tests

`test.py` is a `unittest` suite of Flask test-client checks: every page route returns 200 and renders, and the add/edit/issue/import/member forms behave on valid and invalid input. It points at `librarytestdb` (with `root`/`root` credentials hardcoded in `setUp`).

```bash
python test.py
```

## Heads-up: filenames in this archive

This copy was pulled into a portfolio and the files were renamed to a hyphen/lowercase convention, which broke the references the code expects. To actually run it you'd need to rename back:

- `setup_db.py` reads `LibraryDB.sql` / `LibraryTestDB.sql`, but the files here are `library-db.sql` / `library-test-db.sql`.
- `app.py` calls `render_template("add_book.html")`, `"add_member.html"`, `"edit_book.html"`, etc., but the template files here use hyphens (`add-book.html`, `add-member.html`, …).
- Includes are referenced as `_formhelpers.html` / `_messages.html` / `_navbar.html` but stored as `-formhelpers.html` / `-messages.html` / `-navbar.html`.

The code itself is unchanged from the original submission; only the filenames drifted.

## Scope

A hiring-test project, not production software. The Flask secret key is the literal string `"secret"`, DB credentials for the tests are hardcoded, and the return page's day-count charge means an item held under 24 hours is free. It's a solid demonstration of Flask + MySQL CRUD, form validation, transactional stock/debt logic, and an external API integration.
