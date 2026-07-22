# Scientific Calculator (Android)

A single-activity Android calculator app written in Java. Basic arithmetic plus a set of scientific functions (log, ln, powers, roots, trig, factorial), wired to button taps.

## What it is

One `MainActivity` holds all the logic. Every button in the layout points at a public `onClick` method (`btn_0`, `btn_add`, `btn_sin`, `btn_equal`, and so on). Digits get appended to the display as a string; pressing an operator stashes the current value and the chosen sign; pressing `=` parses the operand(s) to `Double`, runs the operation, and writes the result back to the display.

It's a learning project — the classic build-a-calculator exercise, extended with scientific functions. The source package is `com.dataflair.scientificcalc` (it started from a DataFlair tutorial).

## Operations

Binary (need a value, the operator, then a second value):

- `+`, `-`, `*`, `/`
- `xⁿ` — power, via `Math.pow`

Unary (enter a value, pick the function, press `=`):

- `log` — base-10, `Math.log10`
- `ln` — natural log, `Math.log`
- `√` — square root, `Math.sqrt`
- `sin`, `cos`, `tan` — `Math.sin/cos/tan`, **input treated as radians**
- `!` — factorial, computed with an integer loop (the input is truncated to an int)

Editing:

- `.` — decimal point, blocked after one dot is already present per number
- backspace — deletes the last character, resets the dot flag if it removes a `.`
- clear — wipes the display, the stored operand, and the pending sign

## Tech

- Java, Android SDK
- `compileSdkVersion` / `targetSdkVersion` 29, `minSdkVersion` 21
- `androidx.appcompat:appcompat:1.1.0`
- `androidx.constraintlayout:constraintlayout:1.1.3`
- Gradle build (`app/build.gradle`)

No third-party math libraries — everything runs on `java.lang.Math`.

## Build & run

From the project root (`scientific-calculator/`):

```bash
./gradlew assembleDebug        # build the debug APK
./gradlew installDebug         # build + install on a connected device/emulator
```

Or open the project in Android Studio and hit Run. The output APK lands in `app/build/outputs/apk/`.

There's no desktop/CLI entry point — this is an Android UI app and needs a device or emulator.

## Example

Multiply 6 by 7:

1. Tap `6`
2. Tap `×` (display clears, sign box shows `×`)
3. Tap `7`
4. Tap `=` → display shows `42.0`

Sine of a value:

1. Tap `sin`
2. Enter `1` (radians)
3. Tap `=` → display shows `0.8414709848078965`

## Things worth knowing

- **One operation at a time.** There's no expression parser and no operator precedence. It stores a single pending operator and applies it on `=`; chaining like `2 + 3 * 4` isn't supported.
- **Results are always doubles**, so integer math shows a trailing `.0` (`42.0`, not `42`).
- **Trig is in radians**, not degrees — there's no degree/radian toggle.
- **Divide by zero** returns Java's `Infinity` rather than an error message.
- **Factorial** casts the input to an `int` (`Integer.parseInt`) before looping, so decimals are truncated and large inputs overflow the double.
- **Input guarding is light.** `=` catches an empty display, a missing operator, and a missing first operand for the four basic ops (shows `Error!`), but doesn't validate domains — e.g. `√` or `log` of a negative gives `NaN`.
- `sign` is compared with `==` and `switch` on strings; it works because the values are literals set in code, not something to copy into new code.

## Scope

Practice project, not a production calculator. It's a clean example of Android view binding, `onClick` handlers, and calling `Math` functions — good for learning, not for serious computation.
