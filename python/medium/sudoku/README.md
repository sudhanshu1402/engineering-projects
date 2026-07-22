# Sudoku

A playable Sudoku board in a pygame window, with a backtracking solver that animates itself as it searches.

## What it is

A single-file pygame app (`sudoku.py`). It opens a 500x500 window drawn as a 9x9 grid. You can click or arrow-key to a cell, type a digit to fill it (rejected if it breaks Sudoku rules), or hit Enter to let the solver finish the board for you. The solve isn't instant — it draws every trial value and every backtrack with short delays, so you watch the recursion crawl across the grid.

It's a learning-scale project: no puzzle generator, no menus, no win detection beyond "the solver returned true." One puzzle is hardcoded.

## Stack

- Python
- [pygame](https://www.pygame.org/) — window, drawing, input, timing

That's the only dependency.

## Run

```bash
pip install pygame
python sudoku.py
```

The `.replit` file runs `python 'Sudoku.py'` if you open it on Replit.

## Controls

| Input | Action |
|-------|--------|
| Mouse click | Select the cell under the cursor |
| Arrow keys | Move the selected cell |
| `1`–`9` | Fill the selected cell (only if the value is legal; illegal entries are rejected and print `wrong ! ...`) |
| `Enter` | Run the backtracking solver on the current board |
| `d` | Load the default puzzle |
| `r` | Clear the board to all zeros |
| Window close | Quit |

## How it works

- `defaultgrid` is the 9x9 board; `0` means empty. Filled cells are drawn on yellow tiles, and every third grid line is thick to mark the 3x3 boxes.
- `validvalue(m, k, l, value)` checks a candidate against its row, its column, and its 3x3 box — the standard Sudoku constraint.
- `solvegame(defaultgrid, i, j)` is a recursive backtracker: it skips over pre-filled cells, tries `1`–`9` in the first empty cell, recurses on success, and undoes the guess on failure. After each guess and each undo it clears the window, redraws, and calls `pygame.time.delay(...)` — that's what makes the search visible instead of instant.
- The main `while` loop handles events, applies typed values through the same `validvalue` check, and triggers a solve when Enter sets the flag.

## Honest notes / quirks

This was written to practice pygame and backtracking, and it shows in a few places:

- The grid is indexed as `defaultgrid[x][z]` where `x` is the horizontal coordinate, so rows and columns are effectively transposed relative to how you'd read the printed list. It's internally consistent but confusing to read.
- Arrow-key movement only changes `x` (Up and Down do the same thing as Left/Right), so vertical navigation via keyboard doesn't really work.
- Error/status messages (`wrong!`, `game finished`) are blitted at y=570, below the 500px-tall window, so they don't actually show.
- The default puzzle is a fixed board; there's no random generation.

If you want to extend it, the obvious next steps are fixing the y-offset on the status text, correcting Up/Down navigation, and adding a real "board complete" check.
