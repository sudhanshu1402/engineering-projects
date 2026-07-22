# Tic Tac Toe

A clickable two-player Tic Tac Toe game built with pygame. Not a CLI — it opens a window, you click cells, and it draws X and O sprites.

## What it does

Two humans share one keyboard/mouse and take turns. Click a cell to drop your mark (X goes first, then it alternates). The game detects wins across rows, columns, and both diagonals, draws a red line through the winning three, and shows the status ("X's Turn", "O won!", "Game Draw!") in a bar below the board. After a win or draw it pauses 3 seconds and resets to a fresh board.

There is no AI opponent — both X and O are played by people.

## Stack

- Python 3
- [pygame](https://www.pygame.org/) — the only dependency (window, drawing, image loading, event loop)

Image assets in this folder:
- `x.png`, `o.png` — the marks (scaled to 80x80 at load)
- `tic-tac-opening.png` — splash screen shown for 1 second on start/reset

## Run

```bash
pip install pygame
python tic_tac_toe.py
```

Run it from inside this directory — the script loads the PNGs by relative path.

### Two things to fix before it runs

The script as committed points at filenames that don't match what's on disk:

1. `tic_tac_toe.py` loads `"tic tac opening.png"` (spaces), but the file is `tic-tac-opening.png` (hyphens). Either rename the file or change the string on the `pg.image.load` line.
2. `.replit` runs `python 'Tic Tac Toe.py'`, but the script is `tic_tac_toe.py`. Fix the run command if you use Replit.

Fix those and it launches.

## How it works

- **Board state** is a 3x3 list of lists (`TTT`) holding `"x"`, `"o"`, or `None`.
- **Click mapping** (`userClick`) converts mouse x/y into a 1-3 row/col by comparing against thirds of the 400px board. A move only registers if the target cell is empty.
- **Win check** (`check_win`) scans all three rows, all three columns, and both diagonals after every move, then draws the winning line and updates the status text.
- **Draw** is declared when every cell is filled and no winner was found.
- **Game loop** runs at 30 fps, handles quit and mouse-down events, and calls `reset_game` once a result is in.

The window is 400x500 — a 400x400 board plus a 100px status bar underneath.

## Scope

Practice project. Small, single-file, no tests, no packaging. Local hot-seat only. Good for learning pygame's event loop, blitting, and simple game state — not a polished release.
