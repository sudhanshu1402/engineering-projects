# Scientific Calculator (Android)

A single-screen Android calculator that does basic arithmetic plus a handful of scientific functions. Built as a learning exercise in native Android (Java + XML layouts), following the DataFlair tutorial.

## What it does

One activity, one screen. You tap a number, an operator, another number, then `=`. The top text view shows your input; a smaller line under it shows the pending operator.

Supported operations:

- Arithmetic: `+`, `-`, `×`, `÷`
- Powers and roots: `xⁿ` (x to the power n), `√` (square root)
- Logarithms: `log` (base 10), `ln` (natural log)
- Trigonometry: `sin`, `cos`, `tan` — operate on the value in **radians**, since they call `Math.sin/cos/tan` directly
- `!` factorial
- Editing: `C` (clear all), backspace (delete last character), decimal point

## Stack

- Java, targeting `com.android.application`
- `compileSdkVersion` 29, `minSdkVersion` 21, `targetSdkVersion` 29
- `androidx.appcompat:appcompat:1.1.0`, `androidx.constraintlayout:constraintlayout:1.1.3`
- UI is a plain `LinearLayout` grid of buttons; each button wires to a handler through the `android:onClick` XML attribute
- No third-party math libraries — everything runs on `java.lang.Math`

## Build & run

Standard Gradle Android project. Open it in Android Studio and run, or from the command line:

```bash
./gradlew assembleDebug        # build the debug APK
./gradlew installDebug         # install on a connected device/emulator
```

The APK lands in `app/build/outputs/apk/debug/`.

> Note: files in this repo were renamed with hyphens for portfolio hosting (`main-activity.java`, `android-manifest.xml`, `activity-main.xml`). Android expects `MainActivity.java`, `AndroidManifest.xml`, and `activity_main.xml`. Rename them back before building. The code itself declares package `com.dataflair.scientificcalc` and references `R.layout.activity_main`.

## How the logic works

State lives in a few fields on `MainActivity`:

- `val_1` holds the first operand, captured the moment you tap an operator
- `sign` is a string tag for the pending operation (`"+"`, `"log"`, `"root"`, etc.)
- `has_Dot` blocks a second decimal point in the current number

Number buttons just append their digit to the input text. Operator buttons stash the current value in `val_1`, clear the display, and set `sign`. When you press `=`, a `switch` on `sign` parses the operands with `Double.parseDouble` and writes the result back to the display.

Example: `5`, `xⁿ`, `3`, `=` -> parses `5` and `3`, calls `Math.pow(5, 3)`, shows `125.0`.

Factorial is the one loop in the file: it reads the number, casts to `int`, and multiplies down to 1.

## Scope and known rough edges

This is a beginner Android project, not a polished app. A few honest caveats:

- Trig functions treat input as radians, not degrees.
- Division by zero produces `Infinity`/`NaN` rather than a caught error.
- Factorial casts to `int` and doesn't guard against negatives or overflow.
- No chained expressions — it's strictly `operand operator operand =`.
- `sign` is compared with `==` on the operand-empty check in `btn_equal`; it works because the same string constants are reused, but it's fragile.
- The `app/src/test` and `app/src/androidTest` folders contain only the default generated test stubs — no real tests.

The app label reads "DataFlair Scientific Calculator" (`strings.xml`), a leftover from the tutorial it was built from.
