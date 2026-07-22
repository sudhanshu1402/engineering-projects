# Speed Typing Test

A small pygame desktop app that times how fast you type a random sentence, then reports your time, accuracy, and words per minute.

## What it does

Shows a splash screen, then a window with a random sentence pulled from `sentences.txt`. You click the input box to start the timer, type the sentence, and press Enter. It then displays:

- Time taken (seconds)
- Accuracy (percent of characters that match, position by position)
- WPM (words per minute)

Click the reset area at the bottom to start over with a new random sentence.

This is a learning project — a single-file pygame exercise, not a polished product.

## Stack

- Python 3
- [pygame](https://www.pygame.org/)

Only pygame is needed. There is no requirements file; install it with:

```bash
pip install pygame
```

## Run

From this directory (the image and text assets are loaded by relative path, so you must run it from here):

```bash
python speed_typing_test.py
```

Note: the `.replit` file points at an old filename (`Speed Typing Test.py`). The actual script is `speed_typing_test.py`.

## How it works

Everything lives in one `Game` class in `speed_typing_test.py`:

- `get_sentence()` reads `sentences.txt`, splits on newlines, and picks a random line.
- `run()` is the main loop. It draws the input box, listens for mouse clicks (to focus the box and start the timer, or to reset) and keystrokes (typing, backspace, Enter to submit).
- `show_results()` computes the three metrics on Enter:
  - Time = `time.time()` at submit minus the timestamp captured when you clicked the box.
  - Accuracy = matching characters divided by sentence length, times 100. Comparison is index-aligned, so a single extra or missing character early on throws off everything after it.
  - WPM = `len(input_text) * 60 / (5 * total_time)`, using the common "5 characters = 1 word" convention.
- `reset_game()` clears state, shows the splash image for one second, draws the heading and a fresh sentence.

## Assets

- `sentences.txt` — the sentence pool (6 lines). Add your own, one per line.
- `type-speed-open.png` — splash screen
- `background.jpg` — window background
- `icon.png` — shown with the results

## Editing the sentences

Just append lines to `sentences.txt`:

```
The quick brown fox jumps over the lazy dog.
```

Each line is one possible prompt.

## Known rough edges

- Accuracy is strict positional matching — no alignment, so deletions/insertions cascade.
- Asset paths are relative, so the app only runs from its own directory.
- Prints results to stdout as well as the window (leftover debug output).
