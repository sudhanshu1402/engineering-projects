# Countdown Timer

A small Tkinter desktop app: enter hours/minutes/seconds, hit a button, and it counts down to zero then fires a desktop notification.

## What it does

A 300x200 window with three entry boxes (hours, minutes, seconds) and an "Activate Timer" button. On click it:

1. Reads the three fields, converts them to a total number of seconds.
2. Counts down once per second, updating the numbers live in the window.
3. When it hits zero, pops a system desktop notification ("TIMER ALERT") via `plyer`, plus a Tkinter "Timer Complete!" info box.

The fields start at `00` as placeholders and clear on first click into them. If a field holds anything non-numeric, it shows an "Enter Valid Time" error.

This is a practice/learning project (following a DataFlair tutorial — the window title still says so).

## Stack

- Python 3
- `tkinter` — GUI (ships with the standard library)
- `plyer` — cross-platform desktop notifications (needs installing)
- `time` — the one-second sleep between ticks

## Run

```bash
pip install plyer
python count_down_timer.py
```

Needs a desktop/display — it opens a real window, so it won't run in a headless shell.

## Notes

- The countdown uses `time.sleep(1)` on the main thread with a manual `window.update()` loop, so the window is frozen during the count (no clean way to close it mid-timer). Fine for a toy; a real version would use `window.after()`.
- `bell.ico` is in the folder but the code doesn't reference it (`app_icon=None` in the notification call).
- Heads-up: `.replit` points at `Count Down Timer.py`, but the actual file is `count_down_timer.py`. Run the command above instead of relying on the Replit config.
- The `if min > 60` hour rollover is slightly off (should be `>= 60`), so 60 minutes displays as `60` rather than rolling to `1` hour — cosmetic only, the total time is still correct.
