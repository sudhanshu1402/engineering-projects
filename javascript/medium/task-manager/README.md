# Editorial Task Manager

A single-page to-do list styled like the front page of a print newspaper.

## What it is

One `index.html` file: markup, CSS, and JavaScript in the same document, no dependencies to install. You type a task, hit Commit (or Enter), and it drops into a list. Each row has "Mark Done" (strikes it through with an animated line and italicizes it) and "Remove". A date stamp in the header shows the current day.

The point of the exercise is the styling and interaction, not the logic. It uses a serif/sans editorial look (Playfair Display for headings and input, Inter for body), a hover-reveal for the action buttons, a strike-through animation on completion, and a small insertion animation when a task is added.

## Tech

- Plain HTML, CSS, and vanilla JavaScript. No framework, no build step.
- Google Fonts (Playfair Display + Inter) loaded from a CDN, so first render needs a network connection for the fonts.

## Run it

Open the file in a browser:

```
open index.html
```

Or just double-click it. There's nothing to build or serve.

## Usage

1. Type into the "Define a new objective..." field.
2. Press Enter or click **Commit** — the task is added to the top of the list.
3. Hover a task to reveal its actions; click **Mark Done** to cross it out (click again to Undo), or **Remove** to delete it.

The list ships with one example row ("Finalize System Architecture Doc") so the empty state isn't blank.

## Notes / scope

This is a learning project. A few honest limitations:

- **No persistence.** Tasks live in the DOM only. Refresh the page and everything resets.
- **Task text is injected via `innerHTML`**, so it isn't escaped. Fine as a local demo; you'd want to sanitize or use `textContent` before putting this anywhere real.
- No editing, reordering, filtering, or counts — add, complete, remove, and that's it.

It's a UI/CSS practice piece, and it does that one thing well.
