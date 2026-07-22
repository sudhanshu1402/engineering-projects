# Online Movie Booking System

A desktop CRUD app for managing a movie catalog, built with Python's Tkinter GUI on top of a SQLite database. A DBMS mini-project.

## What it actually does

Despite the name, this is not a ticket-booking or seat-reservation system. It's a records manager for movies. You get a single window where you can add, view, search, update, and delete movie entries. Each record holds:

- Movie ID
- Movie Name
- Release Date
- Director
- Cast
- Budget (Crores INR)
- Duration (Hrs)
- Rating (out of 5)

Data lives in a SQLite file (`movie1.db`, table `book`) so it persists between runs. The GUI is the front end; all database work is in a separate backend module.

## Stack

- Python 3
- `tkinter` (GUI, ships with the standard library)
- `sqlite3` (database, also standard library)

No third-party dependencies, no build step.

## Files

- `mini_project_backend.py` — SQLite functions: create table, add, view, search, delete, update.
- `mini_project_frontend.py` — Tkinter window, form fields, listbox, and buttons that call the backend.

## Run it

The frontend imports the backend as `MiniProject_Backend`, but the file on disk is `mini_project_backend.py`. Before running, rename the file (or fix the import line) so Python can find it:

```bash
# from this directory
cp mini_project_backend.py MiniProject_Backend.py
python mini_project_frontend.py
```

The table is created lazily; if `movie1.db` doesn't exist yet, add your first record and it gets built.

## Usage

1. Launch the app. A black window titled "ONLINE MOVIE TICKET BOOKING SYSTEM" opens.
2. Fill in the fields on the left (Movie ID is required — the Add button ignores empty IDs).
3. **Add New** saves the record. **Display** lists everything in the database. **Search** filters by the field values you typed. Click a row to load it back into the form, then **Update** or **Delete**. **Clear** empties the form; **Exit** closes the app.

## Notes if you're reading the code

A few rough edges are worth flagging honestly, since this is a learning project:

- **Import name mismatch** — the frontend expects `MiniProject_Backend`; the file is `mini_project_backend.py`. It won't run as-is without the rename above.
- **`MovieData()` is never called** and its `CREATE TABLE` string is missing a closing parenthesis. Table creation actually happens implicitly through `AddMovieRec`'s inserts / the DB file — worth cleaning up.
- **`UpdateMovieData` in the backend is broken** — the SQL has a trailing comma before `WHERE` and doesn't bind the `id`. The frontend sidesteps this entirely: its Update button deletes the selected record and re-adds it rather than calling `UpdateMovieData`.
- **Search uses `OR` across all columns**, so an empty field still matches rows where that column is empty string. It's a broad match, not an exact multi-field filter.

## Scope

This is a college DBMS mini-project demonstrating a GUI wired to a relational database with basic CRUD. It's a single-user desktop tool, not a production booking service — there's no auth, no payments, no seats, and no networking. The ER and schema diagrams below describe the intended data model for the assignment.

## ER Diagram

![ER diagram](https://user-images.githubusercontent.com/99204211/183666646-3062c2ab-689a-4599-9425-4c5b5d0a7784.png)

## Schema Diagram

![Schema diagram](https://user-images.githubusercontent.com/99204211/183666744-006318ca-7802-4f5b-b83c-bb0415f36b62.png)

## Output

![App screenshot](https://user-images.githubusercontent.com/99204211/183666836-c2d6cf10-85ed-4cd2-a29d-255364045e70.png)
