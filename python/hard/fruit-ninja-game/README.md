# Fruit Ninja Game

A mouse-controlled Fruit Ninja clone built with pygame. Fruits fly up from the bottom of the window; move the cursor over them to slice them for points, and avoid the bombs.

## What it does

- Fruits (melon, orange, pomegranate, guava) and bombs launch from below on a parabolic arc.
- Slicing happens on hover: when the mouse position falls inside a fruit's 60x60 box, the fruit swaps to its "half" sprite and you score a point.
- Slicing a bomb costs a life. You start with 3 lives (shown as icons top-right). Lose them all and the game-over screen appears.
- Press any key on the start / game-over screen to begin a round.

It's a single-file learning project (~200 lines) that practices the core pygame loop: sprite loading, per-frame physics, mouse collision, and simple game state (lives, score, restart).

## Stack

- Python 3
- [pygame](https://www.pygame.org/) — the only dependency
- Assets: `back.jpg` (background), `comic.ttf` (font), and PNG sprites under `images/`

## Run

```bash
pip install pygame
python fruit_ninja.py
```

The `.replit` file runs the same command (`python 'fruit_ninja.py'`), so it also runs on Replit.

## How the fruit physics work

Each entity is a dict in the global `data` table with position, velocity, and flags. `generate_random_fruits()` seeds it:

- `x`: random start between 100–500
- `y`: starts at 800 (below the visible 500px window) and moves up
- `speed_x`: random −10..10, gives the diagonal drift
- `speed_y`: random −80..−60, the initial upward thrust
- `t`: a per-fruit tick that adds gravity — `speed_y += 1 * t` each frame, so fruits arc up then fall
- `throw`: only ~25% of generated fruits are actually thrown (`random.random() >= 0.75`); the rest are regenerated

When a fruit falls back past `y = 800` (or was never thrown), `generate_random_fruits()` recycles it with fresh randoms. The loop runs at 12 FPS (`clock.tick(FPS)`).

Collision is a plain bounding-box check against `pygame.mouse.get_pos()` — no click needed, just hover.

## Heads-up: asset filename mismatch

The code loads several sprites with underscores:

```python
pygame.image.load("images/white_lives.png")   # line ~30
"images/red_lives.png"                          # draw_lives calls
"images/half_" + key + ".png"                   # on slice
```

but the files in `images/` are named with hyphens (`white-lives.png`, `red-lives.png`, `half-melon.png`, …). As shipped, `pygame.image.load` will raise `FileNotFoundError` on the first missing name. To run it, either rename the image files to underscores or change the `load` paths to hyphens so they agree.

Also note `images/backgound.jpg` (misspelled, unused) — the background actually loaded is `back.jpg` in the project root.

## Scope

Practice project, not a polished game. Known rough edges beyond the filename issue: `pygame.font.match_font("comic.ttf")` is passed a filename where a font family name is expected (it returns `None`, so `draw_text` falls back to the default font), and the game-over flow leans on globals rather than a state machine. Good for learning the pygame loop; not meant as a finished product.
