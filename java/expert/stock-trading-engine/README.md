# Stock Trading Engine

A tiny Java console program that prints a fake stock ticker. It seeds two symbols, nudges their prices randomly, and prints five updates one second apart.

Despite the name and the "expert" folder, this is a small practice script, not a matching engine or order book.

## What it does

- Holds a `Map<String, Stock>` with two hardcoded stocks: `AAPL` at 150.00 and `GOOG` at 2800.00.
- Each tick, every stock's price moves by a random amount in the range `(-2.5, +2.5)` (`(random.nextDouble() - 0.5) * 5`).
- Prints the new price for each stock, then sleeps 1 second. Runs 5 ticks and exits.

No orders, no buy/sell, no persistence. Just a price walk on a timer.

## Tech

- Plain Java, standard library only (`java.util.HashMap`, `Map`, `Random`).
- No build tool, no dependencies. Single file: `StockTradingEngine.java`.

## Build & run

```sh
javac StockTradingEngine.java
java StockTradingEngine
```

The main class is `StockTradingEngine`, not `Main` (the `.replit` config resolves this automatically by grepping for `public static void main`).

## Example output

```
--- Market Ticker ---
AAPL: $151.83
GOOG: $2798.44
--- Market Ticker ---
AAPL: $149.91
GOOG: $2800.12
...
```

Values are random, so every run differs.

## Scope

Learning exercise. If you wanted to grow it into something real, the obvious next steps are an order book, buy/sell matching, and a way to feed in trades instead of a fixed 5-tick loop.
