# Scientific Calculator

An Android scientific calculator app written in Java. One screen, a grid of buttons, and a display. Tap numbers and an operation, hit `=`, get a result.

## What it does

It's a single-activity Android app that handles both basic arithmetic and a handful of scientific functions:

- Arithmetic: `+`, `-`, `*`, `/`
- Powers and roots: `xⁿ` (`Math.pow`), `√` (`Math.sqrt`)
- Logarithms: `log` (base 10) and `ln` (natural)
- Trig: `sin`, `cos`, `tan` — these take the input in **radians**, not degrees
- Factorial: `!` — parses the input as an integer and multiplies down
- Editing: single-character delete (backspace) and full clear

The math lives entirely in `MainActivity.java`. Each button in the layout wires to an `onClick` handler there (`btn_0`, `btn_add`, `btn_sin`, `btn_equal`, and so on). It's a learning-style Android project, not a published app.

## How it works

The calculator is a small state machine held in a few fields:

- `val_1` — the first operand, captured the moment you press an operator
- `sign` — a string tag for the pending operation (`"+"`, `"log"`, `"power"`, etc.)
- `has_Dot` — guards against typing two decimal points in one number

Pressing a binary operator (`+ - * /`) stashes the current display into `val_1`, clears the display, and shows the operator symbol in a small sign box. Unary operators (`sin`, `log`, `√`, `!`, …) just set `sign` and wait. Pressing `=` runs a `switch` on `sign`, parses the operand(s) with `Double.parseDouble`, computes with `java.lang.Math`, and writes the result back to the display.

A few honest limitations that follow from this design:

- One operation at a time. There's no expression parsing and no operator precedence — you can't chain `2 + 3 * 4` in one go.
- Results are raw `double` output, so you'll see things like `4.0` or floating-point tails.
- Trig functions expect radians.
- Factorial goes through `Integer.parseInt`, so it only works on whole-number input.
- `=` shows `Error!` in the sign box if you press it with no operator or an empty operand, but division by zero and other edge cases aren't specially handled.

## Stack

- Java, Android SDK (`compileSdk` 29, `minSdk` 21, `targetSdk` 29)
- `androidx.appcompat` 1.1.0, `androidx.constraintlayout` 1.1.3
- Gradle with the Android Gradle Plugin 4.0.0 (wrapper included)

## Build & run

You need the Android SDK. Easiest path is to open the folder in Android Studio and run it on an emulator or device.

From the command line:

```bash
# build a debug APK
./gradlew assembleDebug

# install onto a connected device / running emulator
./gradlew installDebug
```

The APK lands in `app/build/outputs/apk/debug/`.

## Usage example

Compute `sin(1.5708)` (roughly sin of 90°, since input is radians):

1. Type `1.5708`
2. Tap `sin`
3. Tap `=`

Display shows `~0.9999996...`.

Compute `2⁵`:

1. Type `2`, tap `xⁿ`
2. Type `5`, tap `=`
3. Display shows `32.0`.

## Notes

- The app label is `DataFlair Scientific Calculator` and the package is `com.dataflair.scientificcalc`, from following a DataFlair tutorial. The Java source sits under a `com/sudhanshusingh/...` folder that doesn't match the declared package, so the source tree would need tidying before a clean Gradle build.
- The `test/` and `androidTest/` folders contain only the default Android `Example*Test` stubs — there are no real unit tests for the calculator logic.
