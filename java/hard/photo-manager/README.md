# Photo Manager ("Manage iT")

An Android app that organizes photos into named categories. You create a category, open it, snap photos with the camera, and the app files each shot under that category with a timestamp and keeps a running count.

## What it does

The app has two screens:

1. **Category list (`MainActivity`)** — the home screen. A floating action button opens a dialog to create a new category (name capped at 45 chars, no leading spaces, no duplicates — category name is the SQLite primary key). Categories are shown in a `RecyclerView`, sorted case-insensitively. Long-pressing a category starts a contextual action mode for multi-select delete.

2. **Category detail (`ShowImagesActivity`)** — opens when you tap a category. A FAB launches the system camera; the captured JPEG is written to `Tag_iT/Images/` on external storage, its metadata is inserted into the database, and the category's image count is bumped. The screen uses a `ViewPager` + `TabLayout` with two fragments: **All Images** (a 4-column grid) and **Tagged Images** (a list). Photos are ordered newest-first by capture timestamp.

Storage is a SQLite database (`myDatabase`) with two tables — `myImages` (per-photo rows: tag, category, image name, file path, created timestamp) and `myCategory` (category name, tag count, image count) — accessed through a custom `ContentProvider` (`MyDataProvider`) and loaded into the UI via `CursorLoader`.

## Tech / stack

- **Java**, Android SDK (`compileSdkVersion 25`, `minSdkVersion 15`, `targetSdkVersion 25`)
- **Gradle** with the Android Gradle plugin `2.2.3` (an old toolchain; this is a circa-2017 project)
- Android **support libraries** (`appcompat-v7`, `design`, `recyclerview-v7`, `cardview-v7`, `support-v4`) at `25.1.0`
- **Glide** `3.7.0` — image loading/decoding for the grids and lists
- **material-dialogs** `0.9.2.3`, **MaterialEditText** `2.1.4`, **TextDrawable** `1.0.1` (colored letter tiles / material UI bits)
- Storage: **SQLite** behind a `ContentProvider`; camera capture via `MediaStore.ACTION_IMAGE_CAPTURE` and `FileProvider`

Dependencies pull from `jcenter()` and `jitpack.io`.

## Build & run

Requires the Android SDK and build tools `25.0.2`. From the project root:

```bash
./gradlew assembleDebug        # build the debug APK
./gradlew installDebug         # build and install on a connected device/emulator
```

The output APK lands in `app/build/outputs/apk/`. Because the toolchain is old, building on a current machine will likely mean installing legacy build tools / a matching Gradle version, or bumping the plugin and support-library versions yourself. On the device the app requests `CAMERA` and `WRITE_EXTERNAL_STORAGE` permissions the first time you open a category.

## How the pieces fit

- `MainActivity` — category list, create/delete categories, hosts the search menu item.
- `ShowImagesActivity` — per-category screen; camera capture, DB writes, tabs.
- `MyDatabaseHelper` — `SQLiteOpenHelper`; table schema and versioning (drops and recreates on upgrade).
- `MyDataProvider` — `ContentProvider` routing `myImages` and `myCategory` URIs to the two tables.
- `MyViewAdapter` / `SelectableAdapter` — category-row adapter with multi-select support.
- `MyAllImagesViewAdapter` / `MyTaggedImagesViewAdapter` — grid and list adapters for photos.
- `AllImagesFragment` / `TaggedImagesFragment` + `MyViewPagerAdapter` — the two detail tabs.
- `ScrollingFABBehavior` — hides the FAB on scroll.

## Notable details

- **Custom ContentProvider over raw SQLite.** Rather than hitting the database directly, the UI goes through `MyDataProvider` and `CursorLoader`, so list changes propagate via `notifyChange` and reload without manual refresh plumbing.
- **`FileProvider` for camera output.** Captured photos are handed to the camera via a content URI (`${applicationId}.provider`) declared in the manifest and `provider_paths.xml`, the correct pattern for sharing file URIs across apps.
- **Random material accent per screen.** Each activity picks a random Material color for the toolbar, status bar, and FAB on launch.

## Scope / honesty notes

This is a learning-grade project, and it shows in a few places:

- The search bar in `MainActivity` is inflated but not wired — `onQueryTextChange` / `onQueryTextSubmit` just return `false`.
- The "share category" contextual action is a `// TODO` stub.
- `onUpgrade` in `MyDatabaseHelper` **drops both tables** and recreates them, so a schema version bump wipes all saved data.
- The declared package is `com.example.anujsharma.manageit` (and the provider authority has a typo, `magnageit`), while the source lives under a `sudhanshusingh` directory — this was forked from someone else's code, so the package names don't match the folder.
- No meaningful tests ship with it; the `androidTest`/`test` files referenced in the tree are the default Android Studio placeholders.

Treat it as a hands-on exercise in Android fundamentals — RecyclerView, ContentProvider, SQLite, ViewPager/tabs, camera + FileProvider — rather than a finished product.
