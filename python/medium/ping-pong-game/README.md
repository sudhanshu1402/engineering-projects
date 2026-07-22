# Ping Pong

A two-player Pong clone built with Python's `turtle` graphics module. Practice project for classes, coordinate math, and keyboard-driven game loops.

## What it does

Classic Pong. A ball bounces around an 800x800 window. Each player controls a paddle and tries not to let the ball pass. When the ball goes off one side, the opposite player scores a point. The ball speeds up slightly every time it's hit, so rallies get harder the longer they last.

There's no win condition or exit key — the game runs until you close the window.

## Controls

| Player | Up | Down |
|--------|----|------|
| Left   | `w` | `s` |
| Right  | `Up` arrow | `Down` arrow |

## Stack

- Python 3 (standard library only)
- `turtle` for rendering, `time` for the frame delay

No external dependencies. `turtle` ships with CPython, so nothing to install — but it needs a display, so it won't run in a headless terminal.

## Run

```bash
python ping_pong.py
```

Note: the included `.replit` file points at `python 'Ping Pong.py'`, which doesn't match the actual filename. Run `ping_pong.py` directly.

## How it's put together

Four files, one class each:

- **`ping_pong.py`** — sets up the screen, wires key bindings, and runs the game loop. Handles wall bounces, paddle collisions, and scoring.
- **`ball.py`** — `Ball(Turtle)`. Moves in fixed 10px steps on x and y. `bounce_x` / `bounce_y` flip direction; `bounce_x` also multiplies `ball_speed` by 0.9 (smaller sleep = faster). `reset_pos` recenters the ball and restores the starting speed after a point.
- **`paddle.py`** — `Paddle(Turtle)`. A stretched square that moves 60px per key press. Takes a start position so the same class serves both sides.
- **`scoreboard.py`** — `Scoreboard(Turtle)`. Tracks both scores and redraws them at the top of the screen.

A few things worth knowing:

- Animation is manual. `screen.tracer(0)` turns off turtle's auto-refresh, and `screen.update()` is called once per loop for smooth frames.
- Speed control is `time.sleep(ball.ball_speed)` — a smaller value means a shorter pause, so the ball moves faster. That's why `*= 0.9` speeds things up.
- Paddle collision uses `ball.distance(paddle) < 50` combined with an x-position check. Because of Python operator precedence (`and` binds tighter than `or`), the condition reads as `(right paddle hit) or (left paddle hit)`, which is the intended behavior.

## Scope

Learning exercise. No tests, no menus, no configurable difficulty. It's a compact, readable take on Pong to practice OOP with turtle graphics.
