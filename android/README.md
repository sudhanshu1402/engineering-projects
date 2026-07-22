# Android Development Projects

> **Note:** This is part of my public learning archive. For my active, production-grade work, see the pinned repositories on my [GitHub profile](https://github.com/sudhanshu1402).

Native Android apps written in Java during college and self-study. Both use the classic Android Studio / Gradle project layout with Activities, XML layouts, and the old-style `main-activity.java`-per-screen structure. I keep them public to document how I started before moving on to distributed-systems work.

## Projects

| Project | What it is | Stack |
|---|---|---|
| [scientific-calculator](./scientific-calculator) | A calculator app with basic arithmetic plus log, ln, powers, roots, factorial, and trig | AndroidX, `java.lang.Math`, ConstraintLayout |
| [photo-manager](./photo-manager) | A photo organizer that groups images into named categories/tags, backed by SQLite | Android Support libs, SQLite via ContentProvider, RecyclerView, Glide |

## scientific-calculator

Single-activity app. Each button on the layout wires to a public `btn_*` handler in `MainActivity`. Arithmetic works as a two-operand state machine (store operand 1, remember the sign, then compute on `=`). Unary functions (`log`, `ln`, `sin`, `cos`, `tan`, `√`, `!`) operate on the currently displayed number. Trig uses radians (calls `Math.sin`/`cos`/`tan` directly), and factorial parses the input as an int.

- `compileSdkVersion 29`, `minSdkVersion 21`
- Deps: `androidx.appcompat`, `androidx.constraintlayout`
- Source: `app/src/main/java/.../main-activity.java`

## photo-manager

The more involved of the two. You create categories from a floating action button, then open a category to view/add images. Images are captured via the camera (declares `CAMERA` and `WRITE_EXTERNAL_STORAGE` permissions) and shared through a `FileProvider`.

- Two SQLite tables via `MyDatabaseHelper` — one for images (`_id`, tag, category, name, file, created timestamp), one for categories (name, tag count, image count)
- Data access goes through a custom `ContentProvider` (`MyDataProvider`) loaded with a `CursorLoader`
- UI: `RecyclerView` lists/grids with custom adapters, contextual action mode for multi-select delete, `SearchView` in the toolbar, Glide for image loading, random Material toolbar colors per launch
- `compileSdkVersion 25`, `minSdkVersion 15` (pre-AndroidX, uses `com.android.support:*`)

Heads up: this one predates AndroidX and pulls several third-party libs (Glide 3.7, TextDrawable, MaterialEditText, material-dialogs). The Gradle `applicationId` and the Java package paths don't fully match, which is typical of the tutorial-era code it grew from.

## Building

Each project is a standalone Gradle build. From either project directory:

```bash
./gradlew assembleDebug        # build the debug APK
```

Or open the project folder in Android Studio and run it on a device/emulator. Given the SDK versions (25 and 29), these need older build tools than a current Android Studio ships with — treat them as archived rather than something to build fresh today.

## Scope

Learning projects. No tests of substance (only the generated example unit/instrumented stubs), no CI. They're here as a record of where I started with mobile, not as maintained apps.
