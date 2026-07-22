# Kanban.SYS

A single-file drag-and-drop kanban board built with the native HTML5 Drag and Drop API. No framework, no build step, no dependencies.

## What it is

Three columns (To Do, Doing, Done) with cards you drag between them. Everything lives in one `index.html`: markup, CSS, and about 20 lines of JavaScript. It's a practice piece focused on getting native drag-and-drop working cleanly, with a neobrutalist look (thick black borders, hard offset shadows, dot-grid background, Space Grotesk).

## Stack

- Plain HTML, CSS, and vanilla JavaScript
- HTML5 Drag and Drop API (`draggable`, `ondragstart`, `ondrop`, `ondragover`)
- Space Grotesk loaded from Google Fonts (needs internet on first load; falls back to a sans-serif otherwise)

No package.json, no bundler.

## Run it

Open `index.html` in a browser. That's the whole setup.

```
open index.html
```

## How the drag-and-drop works

- Each card sets `draggable="true"` and stashes its own id on drag start via `dataTransfer.setData("text", ev.target.id)`.
- Columns call `ev.preventDefault()` in `ondragover` so they count as valid drop targets.
- On drop, the handler walks up from `ev.target` to the nearest `.column` element, then appends the dragged card into that column's `.column-dropzone`. The upward walk is what stops a card from getting nested inside another card when you drop on top of one.

## Scope / limits

It's a UI exercise, so it stops where the exercise ends:

- No persistence. Refresh and cards snap back to their starting columns.
- Cards are hardcoded in the HTML. There's no add/edit/delete.
- The column count badges (`01`, `02`, `03`) are static labels, not live card counts.
- Uses native drag-and-drop, so it works with a mouse but not touch.
