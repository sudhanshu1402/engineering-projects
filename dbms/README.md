# DBMS Projects

> **Note:** Part of my public learning archive. For active, production-grade work see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

College and self-study work on database-backed applications. Both projects here are Python desktop apps that put a Tkinter GUI on top of a SQLite database, covering schema design, CRUD, and simple relational modeling with foreign keys.

## Projects

| Project | What it is | Stack |
|---|---|---|
| [hospital-management-system](./hospital-management-system) | Front-office desktop app for a hospital: login, patient registration, room allocation, employee records, appointments, and billing across linked tables | Python, Tkinter, SQLite |
| [online-movie-booking-system](./online-movie-booking-system) | Movie-catalog CRUD app: add, view, search, update, and delete movie records through a Tkinter form | Python, Tkinter, SQLite |

## Common stack

- **Language:** Python (standard library only)
- **GUI:** Tkinter / `ttk`
- **Database:** SQLite via the built-in `sqlite3` module

No third-party dependencies, so each project runs with a stock Python 3 install.

## Running

Each project is self-contained. From inside a project folder:

```bash
# Hospital Management System
python login.py        # login screen -> main menu -> forms

# Online Movie Booking System
python mini_project_frontend.py
```

The hospital app ships with a pre-populated `hospital-db.db`; its `database.py` holds the `CREATE TABLE` statements (mostly commented out) used to build the schema. Login credentials are hard-coded in `login.py` (`admin`/`1234` or `root`/`4321`).

## Scope

These are learning projects. Credentials are hard-coded, there's no input validation to speak of, and the movie-booking backend has a couple of known SQL typos (a missing closing paren in `CREATE TABLE`, a stray comma in `UPDATE`). Kept public as-is to document the progression, not as production code.
