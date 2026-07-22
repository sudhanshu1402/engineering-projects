# Manage iT

An Android photo organizer. You create named categories, snap photos into them with the camera, and the app files each shot under its category in a local SQLite database.

## What it does

The app has two screens:

- **Categories** (`MainActivity`) — a scrollable list of categories you create. A floating action button opens a dialog to add a new one. Each category tracks its image count. Long-press enters a selection mode where you can pick multiple categories and delete them.
- **Images** (`ShowImagesActivity`) — opened by tapping a category. A tab layout with a ViewPager hosts two views of that category's photos ("all images" grid and a "tagged images" list). The FAB fires the system camera; the captured photo is saved to `Tag_iT/Images/` on external storage, recorded in the database against the current category, and the category's image count is bumped by one.

Data flows through a custom `ContentProvider` (`MyDataProvider`) that sits over the SQLite helper, and the UI is fed by `CursorLoader`s so lists refresh when the underlying tables change.

This is a learning project (Android fundamentals: ContentProvider, SQLite, CursorLoader, RecyclerView, FileProvider, runtime permissions). It is not a finished product — see the scope note below.

## Data model

Two tables in `MyDatabaseHelper` (database `myDatabase`, version 5):

- `myCategory` — `categoryName` (primary key), `tagCount`, `imageCount`.
- `myImages` — `_id`, `tagName`, `categoryName`, `imageName`, `imageFile` (path), `imageCreated` (timestamp).

`onUpgrade` drops and recreates both tables, so bumping the version wipes existing data.

## Stack

- Java, Android SDK. `compileSdkVersion 25`, `minSdkVersion 15`, `targetSdkVersion 25`.
- Old Android Support Libraries (`appcompat-v7`, `design`, `recyclerview-v7`, `cardview-v7`, `support-v4`) at 25.1.0 — this predates AndroidX.
- Third-party libs from `build.gradle`:
  - Glide 3.7.0 (image loading)
  - `com.amulyakhare:textdrawable` (color generation for the material toolbar/FAB tinting)
  - `com.rengwuxian.materialedittext` (the category-name input field)
  - `com.afollestad.material-dialogs`
- Tests: JUnit 4.12 and Espresso 2.2.2 stubs only (`ExampleUnitTest`, `ExampleInstrumentedTest` — the default template tests, no real coverage).

## Build & run

This directory is the `app` module of a Gradle Android project. From the project root (the folder containing the top-level `build.gradle` and `settings.gradle`):

```bash
./gradlew assembleDebug        # build the debug APK
./gradlew installDebug         # build and install on a connected device/emulator
```

Or open the project in Android Studio and run the `app` configuration. You need a device or emulator with a camera; the app requests `CAMERA` and `WRITE_EXTERNAL_STORAGE`/`READ_EXTERNAL_STORAGE` at runtime.

Note: the toolchain here is old (SDK 25, build tools 25.0.2, support libraries). A modern Android Studio / Gradle setup will likely need the SDK/build-tools versions and dependencies updated before it compiles.

## Usage example

1. Launch the app. The categories screen is empty.
2. Tap the FAB, type a category name (e.g. `Receipts`), tap **Add**. Names can't be empty, can't start with a space, and cap at 45 characters; duplicates are rejected.
3. Tap the `Receipts` category. Tap the FAB to open the camera, take a photo. It's saved and the category's image count increments.
4. Back on the categories screen, long-press a category to select it, then use the contextual action bar to delete.

## Notable details

- **FileProvider for camera output.** Photos are captured via `ACTION_IMAGE_CAPTURE` with a `content://` URI from a `FileProvider` (`${applicationId}.provider`), rather than a raw `file://` URI. `StrictMode` VM policy is also relaxed in `ShowImagesActivity`.
- **Reactive lists.** `MainActivity` and `ShowImagesActivity` implement `LoaderManager.LoaderCallbacks<Cursor>`; the provider calls `notifyChange` on insert/update/delete so the loaders re-query automatically.
- **Random material accent.** Each activity picks a random material color (via `ColorGenerator`) on create and tints the toolbar, status bar, and FAB with it.
- **Selection mode.** Category multi-select is built on a reusable `selectable-adapter` base class and the support `ActionMode`.

## Scope / honesty notes

- The code package is `com.example.anujsharma.manageit` (its original author), even though the folder lives under a `sudhanshusingh` path.
- The manifest and Java files use the older un-namespaced filenames (`android-manifest.xml`, `activity-main.xml`, etc.) as stored in this repo; a real Android build expects `AndroidManifest.xml` and underscore-named resources — treat this copy as source-of-record, not a drop-in buildable tree.
- Unfinished pieces are visible in the code: category **share** is a `// TODO` no-op, the settings/about menu items do nothing, and the tests are the untouched project template stubs.
- The provider's declared authority (`com.example.anujsharma.magnageit`, note the typo) and the FileProvider authority differ; the app relies on that spelling consistently.
