# Bank Management

A small command-line bank simulator in C++. Create accounts, deposit, withdraw, and check balances from a menu loop.

## What it does

One `main.cpp` file. Accounts live in a `std::map<int, BankAccount>` keyed by an auto-incrementing integer ID, so everything is in memory and gone when the program exits. A `BankAccount` class holds an owner name and a balance and enforces two rules: deposits must be positive, and you can't withdraw more than the current balance.

The menu runs until you pick Exit:

1. Create Account
2. Deposit
3. Withdraw
4. Show Balance
5. Exit

## Build & run

```
g++ -std=c++17 main.cpp -o main
./main
```

## Example

```
1. Create Account
2. Deposit
3. Withdraw
4. Show Balance
5. Exit
Target: 1
Enter name: Alice
Account created with ID: 1

Target: 2
Enter ID: 1
Amount: 500
Deposited: 500

Target: 3
Enter ID: 1
Amount: 900
Insufficient funds.

Target: 4
Enter ID: 1
Account: Alice | Balance: $500

Target: 5
```

## Notes

- Names are read with `std::cin >> name`, so it takes a single token — "Alice Smith" would only capture "Alice".
- No persistence, no authentication, no currency formatting beyond a `$` prefix. Data resets on every run.
- Any menu choice that isn't 1-4 falls through to Exit.

Practice project for OOP and `std::map` in C++, not a real banking system.
