# Bank System

A small console banking program in C that stores accounts in a binary file. Practice project for file I/O with `struct` records.

## What it does

Two operations behind a text menu:

- **Create** — reads an account number, name, and balance, appends the record to `bank.dat`.
- **Display All** — reads every record back from `bank.dat` and prints them.

Each account is a fixed-size `struct`:

```c
typedef struct {
    int accNo;
    char name[30];
    float balance;
} Account;
```

Records are written with `fwrite` and read with `fread`, so `bank.dat` is raw binary, not text. The file persists between runs, so accounts you create stick around.

## Build & run

`.replit` compiles with:

```sh
gcc $(find . -name '*.c') -o main
./main
```

Or directly:

```sh
gcc main.c -o main
./main
```

## Example

```
1. Create
2. Display All
3. Exit
> 1
Enter Account No, Name, Balance: 101 Alice 500.50
Account Created.

1. Create
2. Display All
3. Exit
> 2

--- All Accounts ---
Acc: 101 	 Name: Alice 	 Bal: 500.50
```

Any menu choice other than 1 or 2 exits.

## Scope / caveats

This is a learning exercise, not a real ledger. Known limits worth knowing if you read the code:

- Name input uses `scanf("%s")`, so names with spaces won't parse correctly (only the first word is read).
- `createAccount` doesn't check whether `fopen` succeeded before writing.
- No update, delete, deposit/withdraw, or lookup by account number — just append and dump-all.
- Balance is a `float`, fine for a demo but not what you'd use for real money.
