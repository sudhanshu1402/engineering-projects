# Python

Practice projects in Python, kept from college and early self-study. Small scripts up to a full Flask web app, sorted by how hard they were to build at the time.

> Part of a public learning archive. For current production work, see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

## How this is organized

Four folders by difficulty: `easy/`, `medium/`, `hard/`, `expert/`. Each subfolder is one self-contained project with its own README. Most were built on Replit, so many carry a `.replit` run file alongside the source.

Most GUI/game projects use `pygame`, `tkinter`, or `turtle`. The two computer-vision projects use OpenCV. There's no shared dependency file — each project pulls its own libraries, listed below.

## Projects

### easy

| Project | What it does | Stack |
|---|---|---|
| [01-hello-world](easy/01-hello-world/) | Placeholder slot for the classic first exercise. README only, no script yet. | — |
| [bmi-calculator](easy/bmi-calculator/) | Reads height and weight from input, prints BMI and a category (underweight/healthy/overweight/obese). ~15 lines. | stdlib |
| [count-down-timer](easy/count-down-timer/) | Desktop countdown timer with a Tkinter UI that fires a system notification when time is up. | `tkinter`, `plyer` |
| [currency](easy/currency/) | Live currency-rate viewer with plotted charts and background refresh workers. The heaviest "easy" one. | `PyQt5`, `pyqtgraph`, `requests` |
| [tic-tac-toe](easy/tic-tac-toe/) | Two-player Tic-Tac-Toe with click-to-place, win/draw detection, and reset. | `pygame` |

### medium

| Project | What it does | Stack |
|---|---|---|
| [2048](medium/2048/) | The 2048 sliding-tile game. Grid logic (stack/combine/transpose) plus a colored Tkinter board; colors live in `colors.py`. | `tkinter` |
| [circo](medium/circo/) | Reads lat/long/radius rows from `input.txt` and generates a KML file drawing a circle at each point. | `simplekml` |
| [ping-pong-game](medium/ping-pong-game/) | Two-paddle Pong with a scoreboard, split across `paddle.py`, `ball.py`, and `scoreboard.py`. | `turtle` |
| [speed-typing-test](medium/speed-typing-test/) | Timed typing test that pulls a random line from `sentences.txt` and reports WPM. | `pygame` |
| [sudoku](medium/sudoku/) | Playable Sudoku board plus a backtracking auto-solver, with cell highlighting and input validation. | `pygame` |
| [library-management-system](medium/library-management-system/) | Full CRUD web app for members and books, backed by MySQL. Includes a `dev-hiring-test` variant and SQL seed files. | Flask, `flask_mysqldb`, `wtforms` |

### hard

| Project | What it does | Stack |
|---|---|---|
| [fruit-ninja-game](hard/fruit-ninja-game/) | Slice falling fruit, avoid bombs, track lives and score, with a game-over screen. Sprite art under `images/`. | `pygame` |
| [uno](hard/uno/) | Command-line UNO against the computer. `Card`/`Deck`/`Hand` classes model the full ruleset. | stdlib |

### expert

| Project | What it does | Stack |
|---|---|---|
| [color-detection](expert/color-detection/) | Open an image, double-click any pixel, and it names the nearest color from `colors.csv` with RGB values. | `opencv-python`, `pandas` |
| [gender-&-age-detection](expert/gender-&-age-detection/) | Detects faces in an image and predicts age range and gender using pretrained DNN models. See note below. | `opencv-python` |
| [keyboard-jump-game](expert/keyboard-jump-game/) | Type the shown word before your character falls; words come from `words.txt`. | `pygame` |

## Running a project

Each project runs on its own. In general:

```bash
cd <difficulty>/<project>
pip install <libs listed above>
python <script>.py
```

Two need extra setup:

- **color-detection** takes an image path: `python color_detection.py -i colorpic.jpg`, then double-click a pixel.
- **library-management-system** needs a running MySQL instance; load the included `library-db.sql` (or `library-test-db.sql`) and set the DB connection in `app.py` before starting Flask.

## Notes

- **gender-&-age-detection** expects pretrained Caffe model files (face detector, `age_net`, `gender_net`) that are **not** committed here. Download them separately or the script won't run.
- **01-hello-world** currently holds only a README — no source file yet.
- These are learning exercises. No tests, no CI. They're kept public to show the progression, not as polished libraries.
