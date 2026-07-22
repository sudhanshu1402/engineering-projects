# Trading Simulator

A tiny command-line stock trading toy in C++. Buy shares from a fixed three-stock market with a starting cash balance and watch prices jitter.

## What it does

Runs a text menu loop. You can:

1. Show the market (prints each stock's price, nudging it by a small random amount each time)
2. Buy shares (checks you have enough cash, then debits your balance and adds to your holdings)
3. Show your portfolio (cash left plus share counts per symbol)
4. Exit

The market is hardcoded to three symbols at fixed opening prices: AAPL ($150), GOOGL ($2800), TSLA ($700). You start with $10,000. There's no sell option — this is a learning exercise in classes, `std::map`, and a menu-driven loop, not a real trading engine.

## Stack

- C++17, standard library only (`<iostream>`, `<vector>`, `<map>`, `<string>`, `<random>`)
- No external dependencies

## Build & run

```bash
g++ -std=c++17 main.cpp -o main
./main
```

## Example

```
1. Market
2. Buy
3. Portfolio
4. Exit
> 1

--- Market ---
AAPL: $150.3
GOOGL: $2799.5
TSLA: $700.8
> 2
Symbol Qty: AAPL 10
Bought 10 AAPL
> 3

--- Portfolio ---
Cash: $8497
AAPL: 10
> 4
```

## Notes

- Price "movement" uses `rand()` (never seeded), so the sequence is the same every run.
- The market map keys are iterated in alphabetical order because it's a `std::map`, not insertion order.
- Buying an unknown symbol prints `Stock not found.`; buying more than you can afford prints `Insufficient funds.`
- Scope is deliberately minimal: no selling, no persistence, no real market data.
