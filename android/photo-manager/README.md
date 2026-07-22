# Photo Manager (Manage iT)

An Android app for organizing photos into named categories. You make a category, shoot photos into it with the camera, and browse them back in a list or grid. Photo metadata lives in a local SQLite database behind a ContentProvider; the image files sit on external storage.

This is a learning-era Android project (2017 support-library stack, `compileSdk 25`). It works, but it predates AndroidX, Kotlin, and scoped storage.

## What it does

- **Categories** — The main screen (`MainActivity`) lists categories in a `RecyclerView`. A FAB opens a Material dialog to create one; each category name is unique (it's the primary key), so duplicates are rejected. Long-press a row to enter action mode and delete selected categories.
- **Capture into a category** — Tapping a category opens `ShowImagesActivity`. Its FAB fires an `ACTION_IMAGE_CAPTURE` intent, saves the photo to `.../Tag_iT/Images/` with a timestamped name (`TAG_IT<yyyyMMdd_HHmmss>.jpg`), records a row in the database, bumps the category's image count, and opens the shot in a viewer.
- **Two views of a category** — A `TabLayout` + `ViewPager` swaps between an "all images" grid and a "tagged images" list, both backed by the same cursor loaded newest-first.
- **Search field** — There's a `SearchView` in the main toolbar, but its query callbacks are stubs, so search doesn't filter yet.

## Stack

- Java, Android SDK (`minSdk 15`, `target/compileSdk 25`, build tools 25.0.2)
- Android Gradle Plugin 2.2.3, Gradle wrapper
- `com.android.support` v25.1.0 — appcompat, design, recyclerview, cardview, support-v4
- [Glide](https://github.com/bumptech/glide) 3.7.0 for image loading
- [TextDrawable](https://github.com/amulyakhare/TextDrawable) 1.0.1 for colored letter tiles
- [MaterialEditText](https://github.com/rengwuxian/MaterialEditText) 2.1.4 and [material-dialogs](https://github.com/afollestad/material-dialogs) 0.9.2.3 for input UI

## Data model

Two SQLite tables (`MyDatabaseHelper`, database version 5):

- `myCategory` — `categoryName` (PK), `tagCount`, `imageCount`
- `myImages` — `_id`, `tagName`, `categoryName`, `imageName`, `imageFile`, `imageCreated` (defaults to `CURRENT_TIMESTAMP`)

`MyDataProvider` is a `ContentProvider` that routes two URIs (`.../myImages` → category table, `.../myCategory` → image table — the base-path names are swapped relative to what they query) through a `UriMatcher` and notifies observers so the `CursorLoader`s auto-refresh. Note: `onUpgrade` drops and recreates both tables, so a version bump wipes existing data.

## Build & run

Requires a JDK and the Android SDK (build tools 25.0.2, platform 25). From the project root:

```bash
./gradlew assembleDebug        # build the debug APK
./gradlew installDebug         # build and install on a connected device/emulator
```

The APK lands in `app/build/outputs/apk/`. Because the app writes to external storage and uses the camera, run it on a device or emulator with a camera and grant the storage/camera permissions when prompted.

## Notable details

- Photo capture uses a `FileProvider` (authority `${applicationId}.provider`, paths in `res/xml/provider_paths.xml`) to hand a content URI to the camera — the correct approach for sharing file URIs across apps.
- Toolbar, status bar, and FAB tint are recolored on each launch with a random Material color from TextDrawable's `ColorGenerator`.
- `StrictMode` VM policy is loosened in `ShowImagesActivity` so passing a `file://` URI to the external image viewer doesn't throw.

## Scope / honesty note

This is a portfolio/learning project, not a maintained app. Known rough edges: the toolbar search is wired up but does nothing, the "share category" action is a TODO, runtime permission handling is partial (camera denial isn't handled), and the source package is `com.example.anujsharma.manageit` from the original author. It won't build unchanged against a modern SDK without migrating off the deprecated `com.android.support` libraries.
