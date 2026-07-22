# College Management System

A console CRUD app for student records, written in C++. Add, list, search, edit, and delete students, with everything persisted to a flat binary file.

## What it does

It's a menu-driven terminal program that manages a list of students. Each student has a registration number, a name, and a branch. On start it loads existing records from `College.txt`; on exit it sorts them by registration number and writes them back.

Menu options in `main()`:

- `1` Add a new student (rejects duplicate registration numbers)
- `2` Display all students
- `3` Remove a student by registration number
- `4` Edit a student by registration number
- `5` Search by registration number, name, or branch
- `0` Save to file and (loop) exit

This is a learning project — a standard college-assignment-style records manager. It leans on some old-school C/C++ idioms that are worth knowing about before you run it (see Caveats).

## How it works

- **Data model.** `class student` holds `long int reg` and fixed-size C strings `char name[80]`, `char branch[50]`. Records live in a global `vector<student> v`.
- **Persistence.** `get_file()` and `write_file()` do raw binary I/O — `f.read`/`f.write` with `sizeof(student)` per record. The file is not text; opening `College.txt` in an editor shows binary garbage. A sample `college.txt` is included.
- **Sorting.** `write_file()` runs a hand-written `bubblesort()` over `reg` before saving, so the file stays ordered by registration number.
- **Search.** Three helpers back the search menu: `search_reg` (exact match, returns index), `search_name` and `search_branch` (collect all matching indices via `strcmp`). `student` overloads `operator==` on `reg`.

## Build & run

The repo ships a Dev-C++ `makefile.win` (Windows) and a `.replit` config. The simplest portable build:

```sh
g++ -std=c++17 main.cpp -o main
./main
```

That matches the `.replit` compile line (`g++ -std=c++17 ... -o main`, run `./main`).

On Windows with the included makefile:

```sh
mingw32-make -f makefile.win
```

Note: the file the program reads/writes is `College.txt` (capital C, hardcoded in `get_file`/`write_file`), while the sample committed here is `college.txt`. Rename it to `College.txt` if you want the sample data loaded on a case-sensitive filesystem.

## Usage example

```
			-----------------------------------------
			     Simple College Management System
			-----------------------------------------

			Enter <1> to Add new student
			Enter <2> to Display all student
			Enter <3> to Remove student
			Enter <4> to Edit student
			Enter <5> to Search student
			Enter <0> to Exit

			Enter Your Choice: 1

 Enter name: Sudhanshu
 Enter roll no: 101
 Enter Branch: CSE
 Press [Y] to enter more: n
```

Pick `0` to write everything back to `College.txt` before quitting.

## Caveats

Honest notes if you're going to compile or reuse this:

- **`gets()`** is used for name/branch input. It's removed in C++14 and unsafe (no bounds check). On a modern compiler you'll likely need to swap it for `fgets` or `std::getline`.
- **`system("CLS")` and `system("PAUSE")`** are Windows commands. On macOS/Linux they'll just error out at those points (use `clear` / a read prompt instead).
- **`fflush(stdin)`** is undefined behavior per the standard; it happens to work on some Windows runtimes.
- **Saving only happens on `0`.** Choosing `0` calls `write_file()`, and since `i` is now `0` the `while(i)` loop ends. If you quit any other way, unsaved changes are lost.
- Binary dumps of a class with pointers/padding aren't portable across compilers or architectures — fine for a single-machine exercise, not for real storage.

## Scope

Practice project at the "hard" tier of a C++ exercise set. It's a complete, working CRUD console app with file persistence, but it uses legacy Turbo/Dev-C++ conventions rather than modern C++.
