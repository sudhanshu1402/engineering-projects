# Phonebook System

A small command-line phonebook in C. Add contacts, list them, exit.

## What it does

Menu-driven CLI that keeps name/phone pairs in memory while it runs. Three actions:

1. Add a contact (name + phone)
2. List all contacts
3. Exit

Storage is a fixed array of 100 `Contact` structs. Nothing is saved to disk, so contacts disappear when the program exits. It's a practice exercise in structs, arrays, and a basic input loop.

## Data model

```c
struct Contact {
    char name[50];
    char phone[20];
};
```

Up to 100 contacts (`contacts[100]`), tracked by a `count` counter.

## Build & run

```sh
gcc main.c -o main
./main
```

## Example session

```
1. Add
2. List
3. Exit
> 1
Enter Name: Alice
Enter Phone: 555-1234
Contact added.
1. Add
2. List
3. Exit
> 2

--- Contacts ---
Alice: 555-1234
1. Add
2. List
3. Exit
> 3
```

## Notes and limitations

- Names and phones are read with `scanf("%s", ...)`, so a value stops at the first space. "Alice Smith" would be truncated to "Alice".
- No bounds check on `scanf` input against the 50/20 char buffers, so a very long entry can overflow. Fine for practice, not for real use.
- No search, edit, or delete — only add and list.
- In-memory only; no file persistence.
- The `.replit` config compiles every `.c` in the folder to `main` and runs it, which is how it's set up to run on Replit.

Scope: a beginner C exercise, not a finished tool.
