# Scientific Calculator (Android)

A single-screen Android calculator app that does basic arithmetic plus a handful of scientific functions. Built as a learning project following the DataFlair Android tutorial.

## What it does

One activity, a grid of buttons, two `TextView`s (one for the current input, one small box that shows the pending operator). You tap digits, pick an operation, tap `=`, and the answer replaces the input.

Supported operations (from `MainActivity.java`):

- Arithmetic: `+`, `-`, `×`, `÷`
- Powers and roots: `xⁿ` (`Math.pow`), `√` (`Math.sqrt`)
- Logs: `log` (base 10), `ln` (natural)
- Trig: `sin`, `cos`, `tan`
- Factorial: `!`
- Utility: decimal point, backspace (`DEL`), clear (`C`)

Each button is wired straight to a Java method via `android:onClick` in the layout — `btn_add`, `btn_sin`, `btn_equal`, and so on. There's no expression parser; state lives in a few fields (`sign`, `val_1`, `val_2`, `has_Dot`) and `btn_equal` runs a `switch` on the stored `sign`.

## Stack

- Java, Android SDK
- `compileSdk` 29, `minSdk` 21, `targetSdk` 29
- AndroidX `appcompat` 1.1.0, `constraintlayout` 1.1.3
- Gradle (Android Gradle Plugin 4.0.0)
- Package: `com.dataflair.scientificcalc`

No third-party math library — everything runs on `java.lang.Math`.

## Build & run

From the repo root (`scientific-calculator/`, one level up from this `app/` module):

```bash
./gradlew assembleDebug        # build the debug APK
./gradlew installDebug         # build + install on a connected device/emulator
```

Or open the project in Android Studio and hit Run.

APK lands at `app/build/outputs/apk/debug/app-debug.apk`.

## How the math behaves (worth knowing)

- **Trig is in radians.** `sin`/`cos`/`tan` pass the raw input straight to `Math.sin` etc., so `sin(90)` is *not* 1 — it's `sin(90 radians)`. No degree conversion.
- **Only one operation at a time.** There's no chaining; `2 + 3 × 4` isn't a thing. You compute one binary (or unary) operation, then start over.
- **Factorial truncates.** It does `Integer.parseInt(val_1)` and loops down, so a decimal input is cut to its integer part and large values overflow.
- **Results are raw `Double.toString`.** So integer results show as `5.0`, and division can surface floating-point tails like `0.30000000000000004`.
- **Division by zero** yields Java's `Infinity`/`NaN` rather than an error message.
- Error handling is limited to `btn_equal`: it shows `Error!` if you hit `=` with no operator, empty input, or a missing first operand.

These are the usual rough edges of a tutorial calculator, left as-is.

## Layout of this module

```
app/
├── build.gradle                     # module config, SDK versions, deps
├── proguard-rules.pro
└── src/
    ├── main/
    │   ├── android-manifest.xml     # single MainActivity, LAUNCHER intent
    │   ├── java/.../MainActivity.java
    │   └── res/
    │       ├── layout/activity-main.xml   # button grid + display
    │       ├── drawable/                    # button backgrounds, backspace icon
    │       ├── values/                      # colors, styles, strings
    │       └── mipmap-*/                     # launcher icons
    ├── test/          # ExampleUnitTest (default template stub)
    └── android-test/  # ExampleInstrumentedTest (default template stub)
```

The tests are the stock Android Studio placeholders (`assertEquals(4, 2 + 2)` and the instrumentation package-name check) — no real coverage of the calculator logic.

## Note on file names

Some files in this snapshot were renamed with hyphens for portfolio hosting (`android-manifest.xml`, `activity-main.xml`, and a hyphenated Java source folder). Android's build expects `AndroidManifest.xml`, `activity_main.xml`, and a package-matching folder path, so you'd rename those back to build cleanly. The Java `package` declaration and the `R.layout.activity_main` / `R.id.input_user` references in the code are the source of truth for the intended names.

## Scope

Learning project. It's a working demo of Android event handling and `findViewById` wiring, not a calculator you'd ship. Radian trig, no operator chaining, and raw-double output are all deliberate simplicity, not bugs to hide.
