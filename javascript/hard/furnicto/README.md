# Furnicto

A five-page static website for a fictional interior/home-design studio. Plain HTML, CSS, and jQuery. No build step, no backend.

## What it is

A front-end practice project built from a classic table-less HTML template. It's a marketing-style site for a home-design business, with a jQuery photo gallery on the home page and static content pages for the rest. The point of the exercise was hand-wiring layout, a grid system, and a third-party gallery plugin — not building a real product.

Pages:

| File | What's on it |
|------|--------------|
| `index.html` | Home. Galleriffic thumbnail slideshow, intro copy, and short "Balance / Rhythm / Harmony" design-principle blocks. |
| `information.html` | Emphasis, Proportion and Scale, "About us", mission, and a comments section. |
| `designs.html` | Projects archive — formal dining room, family room, etc. |
| `designers.html` | The studio and a pricing block. |
| `contacts.html` | Contact form, address, and closing copy. |

The header nav and footer are copied across all five pages.

## Stack

- HTML5 (`js/html5.js` shim is bundled for old browsers)
- CSS split into three files:
  - `css/reset.css` — normalize/reset
  - `css/grid.css` — a 12-column grid (`container_12`, `grid_1`…`grid_12`)
  - `css/style.css` — the actual theme (~990 lines)
- jQuery 1.6.2 (`js/jquery-1.6.2.min.js`)
- Gallery plugins:
  - `js/jquery.galleriffic.js` — thumbnail slideshow engine
  - `js/jquery.opacityrollover.js` — fade-on-hover for thumbnails
  - `js/jcarousellite-1.0.1.js` — carousel plugin (bundled)

All dependencies are vendored in `js/`; nothing is fetched from a CDN.

## Run it

No install, no server needed. Open the file directly:

```
open index.html
```

Or serve the folder if you'd rather use `http://` (needed if a browser blocks `file://` script loads):

```
python3 -m http.server 8000
# then visit http://localhost:8000
```

## How the gallery works

The home page slideshow is set up at the bottom of `index.html`. The thumbnail list (`#thumbs ul.thumbs`) is plain HTML — six `<li>` items, each linking a full-size `images/gallery-imgN.jpg` behind a `images/thumb-N.jpg` preview. On `$(window).load`, the inline script:

1. Applies opacity rollover to the thumbnail spans.
2. Calls `$('#thumbs').galleriffic({...})` to turn the list into an auto-playing slideshow that renders into `#slideshow`.

Key options passed to galleriffic: `delay: 7000` and `autoStart: 7000` (7s per slide), `defaultTransitionDuration: 900`, `syncTransitions: true`, and `enableHistory: true`. Because the markup is a real list, the page degrades to a plain gallery of links if JavaScript is off (`ul.thumbs.noscript`).

## Notes

- The search box in the header (`#search-form`) submits to nothing — the button just calls `.submit()` on a form with no action. It's UI only.
- The contact form on `contacts.html` has no backend either.
- `<title>` is empty on every page.
- Footer credit reads "Designed by: Sudhanshu Singh"; the phone number is a placeholder.

## Scope

Learning project. It's a static template site — no framework, no bundler, no tests. Useful as a reference for a jQuery galleriffic setup and a manual 12-column CSS grid.
