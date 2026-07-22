# Weather Dashboard

A glassmorphism weather card UI. Type a city, hit Scan, and it animates in a temperature reading.

## What it does

Single-file front-end demo focused on visual polish, not real data. The interface is the point:

- Frosted-glass panel (`backdrop-filter: blur`) floating over an animated gradient background
- Two blurred colour orbs drifting behind the glass for an atmospheric glow
- A search field with a "Scan" button that reveals the result with a fade-and-slide transition

The weather value itself is **mocked**. `getWeather()` waits 600ms to fake a radar scan, then injects a hardcoded `{ temp: 24, condition: 'Partly Cloudy' }` for whatever city you typed. There's no API call, no fetch, no network — the placeholder text ("Enter coordinates or city...") and the mock comment in the code make the intent clear.

## Tech

Plain HTML, CSS, and vanilla JavaScript in one `index.html`. No build step, no dependencies. Pulls the Plus Jakarta Sans font from Google Fonts over the network.

## Run it

Open the file in a browser:

```
open index.html
```

## Notable bits

- **Animated gradient** — 4-colour linear gradient with `background-size: 400% 400%` cycling via `@keyframes`.
- **Replay-safe reveal** — before re-showing the result it removes the `visible` class, rewrites the DOM, then forces a reflow with `void resultDiv.offsetWidth` so the CSS transition fires again on repeat searches.
- **Empty-input fallback** — city name defaults to "Unknown Sector" when the field is blank.

## Scope

Practice piece for CSS glassmorphism and animation timing. To make it a real dashboard you'd swap the mock block in `getWeather()` for an actual weather API fetch (e.g. Open-Meteo or OpenWeather) and map the response fields onto the same UI.
