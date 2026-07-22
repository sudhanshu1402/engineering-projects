# 2048

A desktop clone of the sliding-tile puzzle game 2048, built with Python's `tkinter`.

## What it is

The classic 2048: a 4x4 grid of tiles that you slide with the arrow keys. When two tiles with the same number touch, they merge into one worth double. Each move spawns a new tile and adds to your score. You win by making a 2048 tile; you lose when the board fills up with no merges left.

It's a learning project — a self-contained GUI game to practice grid manipulation, event binding, and separating game logic from rendering.

## Stack

- Python 3
- `tkinter` (standard library — no third-party dependencies)

## Run

```bash
python 2048.py
```

A window opens and the game starts immediately. Use the arrow keys to play.

## How it works

The board is a 4x4 list of lists (`self.matrix`). Every move is built from four small transformations:

- `stack()` — slides all non-zero tiles toward the left, closing gaps.
- `combine()` — merges adjacent equal tiles leftward and adds the merged value to the score.
- `reverse()` — flips each row left-to-right.
- `transpose()` — swaps rows and columns.

Only "left" is implemented directly (`stack` → `combine` → `stack`). The other three directions reuse it by re-orienting the grid first:

- **Right** — reverse, do the left move, reverse back.
- **Up** — transpose, do the left move, transpose back.
- **Down** — transpose and reverse, do the left move, undo both.

After each move a new `2` or `4` tile is dropped on a random empty cell (`add_new_tile`), the GUI is repainted from the matrix (`update_GUI`), and `game_over` checks for a win (any 2048 tile) or a loss (board full and no horizontal or vertical merges possible).

Colors, fonts, and the per-value tile styling live in `colors.py` as plain dictionaries keyed by tile value, so tweaking the look doesn't touch game logic.

## Files

- `2048.py` — game logic and the tkinter UI.
- `colors.py` — color and font constants.

## Notes / limitations

- The board is fixed at 4x4.
- Score isn't persisted between runs, and there's no high score.
- A move always spawns a new tile even when nothing on the board actually shifted (the original 2048 only spawns on a real move).
- The game-over / win banner is drawn once; there's no restart button — close and re-run to play again.
