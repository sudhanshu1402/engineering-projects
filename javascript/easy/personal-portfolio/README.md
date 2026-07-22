# Personal Portfolio

A single-page personal site for a backend/infrastructure engineer. One `index.html` file, no build step, no dependencies.

## What it is

A static portfolio page. Everything lives in `index.html` — markup, CSS (in a `<style>` block), and a small vanilla-JS scroll animation. It presents four sections: hero, engineering profile, a grid of "core architecture" cards, and a current-research note, plus a footer with contact links.

The visual style is dark with a fixed 50px CSS grid background, an SVG noise overlay, an orange accent, and two Google Fonts (Outfit for display, JetBrains Mono for labels).

## Tech

- Plain HTML + CSS, no framework and no bundler
- CSS custom properties (`:root` variables) for colors, fonts, and edge padding
- CSS grid and flexbox for layout; `clamp()` for fluid type sizes
- One responsive breakpoint at 900px (the two-column grids collapse to one)
- Google Fonts loaded over CDN (Outfit, JetBrains Mono)
- ~15 lines of vanilla JS for scroll-triggered reveals

No `package.json` — there are no dependencies to install.

## Run it

Open the file directly:

```bash
open index.html
```

Or serve it if you prefer a local server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Notable bits

- **Scroll reveals**: elements with class `reveal` start hidden (`opacity: 0`, translated down). A `scroll` listener adds `.active` when an element enters the viewport, fading it in. `reveal()` also runs once on load so above-the-fold content shows immediately.
- **Grid background**: two crossed linear-gradients on `<body>` at `50px 50px` size draw the grid; the hero masks it out at the top with a `mask-image` gradient.
- **Noise overlay**: a fixed full-screen div with an inline SVG `feTurbulence` data-URI at 3% opacity, `pointer-events: none` so it never blocks clicks.
- **Hover effects**: nav/footer links shift to the accent color; the outlined hero word fills in on hover; the architecture cards lift and reveal a top accent bar via a `::before` scaleX transition.

## Scope

Practice project — a hand-written static page, no tooling. The scroll animation uses a raw `scroll` listener rather than `IntersectionObserver`, which is fine at this size. Fonts require a network connection to load.
