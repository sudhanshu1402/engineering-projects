# Quiz Page

A timed multiple-choice quiz that runs entirely in the browser. Five questions, 15 seconds each, instant right/wrong feedback, and a score at the end. Skinned as a "cyberpunk" terminal interface.

## What it does

- Start screen with a set of rules, then a quiz, then a result screen.
- Each question shows four options. Clicking one locks in the answer immediately — you can't change it.
- Correct pick turns green with a check icon; wrong pick turns red with a cross, and the correct option is revealed in green.
- A 15-second countdown per question, plus a pink progress line that fills across the header. If the timer hits zero, the question auto-reveals the correct answer and shows the next button.
- Final screen tallies your score out of 5, with one of three messages depending on how you did (`>3`, `>1`, or lower).

It's a practice project — plain DOM manipulation, no framework, no build step, no persistence. Refreshing the page resets everything.

## Stack

- HTML, CSS, vanilla JavaScript.
- Google Fonts (Rajdhani) and Font Awesome 5, both pulled from CDNs — so it needs an internet connection to look right and to render the check/cross/result icons.

No `package.json`, no dependencies to install.

## Run it

Open `index.html` in a browser. That's the whole setup.

```
open index.html      # macOS
```

## Files

| File | Role |
|------|------|
| `index.html` | Markup for all three screens (info / quiz / result). All the active styling lives in an inline `<style>` block in the `<head>`. |
| `js/questions.js` | The question bank — an array of `{ numb, question, answer, options }` objects. |
| `js/script.js` | All the logic: screen switching, rendering questions, answer checking, timers, scoring. |
| `style.css` | The original blue "Poppins" stylesheet. It is **not linked** — `index.html` deliberately dropped the link and replaced it with the inline cyberpunk theme. Kept in the repo but currently dead. |

## Adding questions

Push another object onto the array in `js/questions.js`, keeping `numb` sequential:

```js
{
  numb: 6,
  question: "Your question here?",
  answer: "The correct option text",
  options: ["Option 1", "Option 2", "Option 3", "The correct option text"],
},
```

`answer` must match one of the `options` strings exactly — the code compares them by text content. The score-message thresholds in `showResult()` (`>3`, `>1`) are hardcoded for a 5-question quiz, so adjust those if you change the count.

## How it works, briefly

- Screens are three absolutely-positioned boxes. JS toggles `activeInfo` / `activeQuiz` / `activeResult` classes to fade the right one in.
- Questions render as HTML strings injected via `innerHTML`; each option gets an inline `onclick="optionSelected(this)"`.
- Answer matching is string comparison (`userAns == correcAns`). On a wrong answer or a timeout, the code loops the options to find and highlight the correct one.
- Two independent `setInterval` timers run per question: one counts the 15 seconds down, the other widens the pink `.time_line` by 1px every 29ms until ~549px.

## Known rough edges

- Loop counters use an undeclared `i` (implicit global) instead of `let i` — works, but it leaks to the global scope.
- Icon markup uses classes `.icon.tick` / `.icon.cross`, but the inline stylesheet has no rules for them, so the tick/cross rely on Font Awesome and inherit generic option colors.
- No shuffling — questions and options always appear in the same order.

Small learning build, not production code. The interesting parts are the dual-timer setup and the pure-DOM screen switching.
