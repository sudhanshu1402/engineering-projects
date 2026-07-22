# Hospital Management

A small C practice program: a menu-driven CLI that stores hospital patient records in a binary file.

## What it does

Runs a loop with three options:

1. Register a patient (ID, name, disease)
2. Show all patients
3. Exit

Each patient is a fixed-size `struct` (id + name + disease). New patients are appended to `patients.txt` in binary form with `fwrite`, and the show command reads them back with `fread` until the end of the file. The data survives between runs because it lives in the file.

```c
struct Patient {
    int id;
    char name[50];
    char disease[50];
};
```

## Build & run

Standard C, no dependencies. From this directory:

```sh
gcc main.c -o main
./main
```

The `.replit` file uses the same steps (`gcc` then `./main`).

## Usage

```
1. Register Patient
2. Show Patients
3. Exit
> 1
Enter ID, Name, Disease: 101 Ravi Fever
Patient recorded.
> 2

--- Patients ---
ID: 101 | Name: Ravi | Disease: Fever
> 3
```

Records are written to `patients.txt` next to the binary. Names and diseases are read with `%s`, so they must be single words (no spaces).

## Scope

Learning exercise for C file I/O with binary structs. It's deliberately minimal — no editing, no deleting, no search, and `addPatient` doesn't check that the file opened. It covers the append-and-read-back pattern and nothing more.
