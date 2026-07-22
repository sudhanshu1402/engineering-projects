# Keyboard Jump Game

A small typing game built with pygame. A word drifts down the screen on a plank; type it correctly before it hits the bottom.

## What it does

A random word from `words.txt` appears near the top and slowly falls. You type it letter by letter:

- Type the whole word correctly and you score points equal to the word's length, then a new word spawns.
- The falling speed bumps up a little (`+0.10`) with every new word, so the game gets harder as you go.
- Type a wrong letter (one that breaks the prefix) and it's game over.
- Let the word reach the bottom of the window and it's also game over.

The score is shown at the top. On game over you see the final score, and pressing any key restarts from the front screen.

## Stack

- Python
- [pygame](https://www.pygame.org/) — window, image rendering, keyboard events, font drawing

Assets bundled in the folder:

- `keyback.jpg` — front/game-over screen background
- `teacher-background.jpg` — in-game background
- `char.jpg` — the character sprite
- `wood-.png` — the plank the word rides on
- `comic.ttf` — font used for all text
- `words.txt` — comma-separated word list the game draws from

## Run it

You need Python and pygame:

```bash
pip install pygame
python keyboard_jump_game.py
```

The script loads images and fonts by relative path, so run it from inside this directory.

Note: the included `.replit` points at `Keyboard Jump Game.py`, but the actual file is `keyboard_jump_game.py` — use the real filename.

## How the code works

It's one file, `keyboard_jump_game.py`, structured around a single `while True` loop:

- `new_word()` picks a random word, resets its x/y position, clears the typed buffer (`yourword`), and increases `word_speed`.
- Each frame the word's `y_cor` grows by `word_speed`, and the background, plank, character, and word are re-blitted.
- On `KEYDOWN`, the pressed key name is appended to `yourword`. If `displayword.startswith(yourword)` the guess is still valid; a full match scores and spawns a new word. Any non-matching key ends the game.
- `game_front_screen()` handles both the start screen and the game-over screen, blocking until a key is released.

## Scope

This is a practice project, so a few rough edges are worth calling out honestly:

- Input uses raw `pygame.key.name(event.key)`, so modifier or non-letter keys get appended to the buffer and will usually trigger a game over.
- The window is a fixed 800x600.
- After a wrong letter the process actually quits (`pygame.quit()`) rather than looping back cleanly.

It's a fun, compact example of a pygame render loop and keyboard-driven state.
