# Currency

A small PyQt5 desktop app that charts historic currency exchange rates against a base currency.

## What it does

The window (titled "Doughnut") shows a line chart of exchange rates over the last 180 days on the left, and a table of currencies with their live rate on the right. You pick a base currency from the toolbar dropdown; the app fetches rates for that base and plots each other currency as a line. Tick the checkboxes in the table to show or hide individual currencies on the chart. Move the mouse across the chart and a vertical marker follows the cursor while the table updates to show the rates for that day.

It's a learning project built around Qt threading and plotting, not a production tool.

## Stack

- **PyQt5** — GUI, threads (`QThreadPool` / `QRunnable`), table model.
- **pyqtgraph** — the plot widget.
- **requests** + **requests-cache** — fetching rates, with an on-disk SQLite HTTP cache (`http_cache`) so repeat requests don't re-hit the network.
- Data source: the old keyless `fixer.io` historic endpoint (`http://api.fixer.io/<date>`).

## Run

```bash
pip install PyQt5 pyqtgraph requests requests-cache
python currency.py
```

There is no `requirements.txt` in the folder; install the four packages above. The `.replit` file runs `python 'Currency.py'` (note the capitalisation mismatch with the actual `currency.py`).

## How it works

- **Progressive fetching.** Rather than requesting day 0, 1, 2… in order, `DATE_REQUEST_OFFSETS` is built with a binary-split (breadth-first bisection) pattern: today first, then the midpoint, then the quarter points, and so on. This fills in a rough shape of the whole 180-day range quickly and refines it, so the chart looks useful before all requests finish.
- **Background worker.** `UpdateWorker` (a `QRunnable`) does the HTTP work off the UI thread and emits `data`, `progress`, `error`, and `finished` signals back to `MainWindow`. Changing the base currency cancels the running worker via a `cancel` signal before starting a new one.
- **Politeness + caching.** After any request that wasn't served from cache, the worker sleeps 1 second before the next one.
- **Incremental redraw.** The plot throttles redraws to at most once per second while data streams in, and reuses existing line objects (`setData`) instead of clearing and replotting.

## Caveat

This targets the free, keyless `fixer.io` endpoint that was deprecated years ago (fixer.io now requires an API key and uses a different host). So the network fetch will likely fail against the live service as written. The code is still a clean, readable example of Qt worker threads, signals, and live plotting.

## Scope

Practice project. Single file (`currency.py`), ~350 lines. No tests, no packaging.
