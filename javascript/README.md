# JavaScript Projects

Frontend practice projects written in plain HTML, CSS, and JavaScript during college and self-study. Kept public as a learning archive.

> For current production-grade work, see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

## What's here

Small, self-contained web projects. Almost everything is vanilla JS with no build step. One project (Furnicto) uses jQuery plugins. Folders are grouped by how hard the project was to build, not by any formal rubric.

Most projects run by opening `index.html` in a browser. No install, no server, no dependencies to fetch.

## Projects

### Easy

| Project | What it is |
|---|---|
| [personal-portfolio](easy/personal-portfolio) | Single-page portfolio site (profile / research / infrastructure sections) with a contact form and responsive layout. One `index.html`. |
| [quiz-page](easy/quiz-page) | Multiple-choice quiz on HTML/CSS terms. Questions live in `js/questions.js`; `js/script.js` handles the 15-second per-question timer, scoring, and result screen via DOM show/hide. |

### Medium

| Project | What it is |
|---|---|
| [task-manager](medium/task-manager) | In-memory to-do app: add, edit, and delete tasks. State is not persisted (no localStorage). |
| [decibell](medium/decibell) | A static UI mockup exported from a design tool — a 3300-line `index.html` full of positioned SVG shapes and PNG assets. Layout export, not an interactive app. |

### Hard

| Project | What it is |
|---|---|
| [furnicto](hard/furnicto) | Multi-page furniture site (home, designs, designers, contacts, information). Uses jQuery with the Galleriffic image gallery and jCarouselLite carousel plugins. |
| [weather-dashboard](hard/weather-dashboard) | "Atmospheric Weather" — a city search with a radar-scan animation. Note: the weather data is mocked (hardcoded values behind a `setTimeout`), not a live API. |

### Expert

| Project | What it is |
|---|---|
| [kanban-board](expert/kanban-board) | Drag-and-drop board with To Do / In Progress / Done columns, built on native HTML5 drag events. |
| [saa-s-dashboard](expert/saa-s-dashboard) | Placeholder — currently only a README, no source code. |

## Running any project

```bash
# from a project folder
open index.html        # macOS
# or just double-click index.html
```

Furnicto and quiz-page load their CSS/JS from local `css/` and `js/` folders, so keep the folder intact when opening.

## Scope

These are learning exercises, not products. Expect inline styles in places, no tests, and no build tooling. The point was to practice DOM manipulation, layout, and small bits of interactivity.
