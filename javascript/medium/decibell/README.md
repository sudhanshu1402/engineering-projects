# Decibell

A static "coming soon" landing page for a concept product called Decibell — a voice/audio sharing platform. The whole page is a fixed 1920×1080 design mockup exported from a design tool to HTML and CSS.

## What this is

A single-screen landing page. Black background, a collage of sliced PNG images, and a subscribe panel. The copy sets the pitch:

- Headline: *"Stand out and be heard, every voice has a value."*
- Brand + tagline: **Decibell** — Speak · Share · Inspire
- A **COMING SOON!** block with an email field, a Subscribe button, and "Subscribe to find out when it's ready."

None of the form controls do anything — the email box and Subscribe button are drawn with SVG rectangles and positioned text, not real `<input>`/`<button>` elements. It's a visual mockup, not a working signup form.

This lives under `javascript/medium/`, but there's no hand-written application JavaScript here. The only script is boilerplate emitted by the export tool (see below).

## How it's built

This is a design-tool export, not code written by hand. The tells:

- CSS custom properties like `--web-view-name`, `--web-view-id`, `--web-enable-scale-up` on a `.mediaViewInfo` block.
- Everything absolutely positioned inside a fixed `#Web_1920___1` canvas (1920px wide).
- Layer artwork sliced into 15 PNGs (`component.png`, `component-1-.png` … `component-14-.png`), each placed by pixel coordinates.
- Shapes (background rectangles, the diagonal line, the divider ticks) rendered as inline `<svg>`.
- Fonts pulled from whatever the OS has: Comic Sans MS, Consolas, Arial, Algerian.

### Files

| File | What it is |
|------|-----------|
| `decibell.html` | Self-contained version — CSS and the export's scaling script are inlined (~3,300 lines). Root element is `#Web_1920___1`. This is the one to open. |
| `decibell.txt` | The original export as HTML. Links out to `Web_1920___1.css` and `Web_1920___1.js` and uses `component__N_.png` image names — none of which match the files on disk, so this one won't render on its own. |
| `web-1920-1.css` | Standalone stylesheet. Matches the `#Web_1920___1` layout used by `decibell.html`. |
| `component*.png` | The sliced layer artwork, each in 1× and `@2x` variants. |

The inline `<script>` in `decibell.html` is a generic `Application` object from the exporter that handles scaling the canvas to the viewport and switching between media-query "views." There's only one view here, so it mostly just scales the artboard.

## Run it

Open `decibell.html` in a browser:

```
open decibell.html
```

No build step, no dependencies, no package manager.

### Known issue: images won't load as-is

The HTML references images as `component__5_.png` (double underscores), but the files on disk are named `component-5-.png` (dashes). Until the names line up, the collage renders as broken image icons. To see it as intended, either rename the files to match the `component__N_.png` pattern, or find-and-replace the `src`/`srcset` values in `decibell.html` to the dashed names.

## Scope

Practice / portfolio piece. It's a static exported mockup — a fixed-size design turned into HTML, not a responsive or interactive front end. Good as a visual reference for the Decibell concept; not a starting point for a real signup flow (there's no form logic, no backend, no reflow below 1920px).
