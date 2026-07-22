# Manage iT

An Android app that groups your photos into named categories. Make a category, open it, snap photos with the camera, and they get saved and tagged to that category. Built on Android's SQLite + ContentProvider stack.

This is the `manageit` source package — the Java classes that make up the app. The Gradle project root is four levels up (`photo-manager/`).

## What it does

- **Main screen** — a scrolling list of categories. Each card shows the category name, an auto-generated round letter avatar (from `TextDrawable`), and counts for tags and images. A floating action button opens a dialog to create a new category.
- **Category screen** — tap a category to open it. A tab layout with two tabs ("ALL" / "TAGS") sits over a `ViewPager`. The FAB fires the system camera; the captured photo is written to `Tag_iT/Images/` on external storage and recorded in the database against the current category.
- **Select and delete** — long-press a category to enter a contextual action mode, multi-select cards, and delete them. Delete is batched: consecutive positions are removed as a range, singles one at a time.
- **Image grid** — the "ALL" tab shows every image in the category in a 4-column grid, loaded with Glide. Tapping an image opens it in the device's default image viewer.

The data model is two SQLite tables behind one `ContentProvider`:

- `myCategory` — category name (primary key), tag count, image count.
- `myImages` — one row per captured photo: tag name, category, file name, file path, created timestamp.

## Stack

- Java, Android SDK (compile/target **API 25**, min **API 15**)
- Android Support Libraries 25.1.0 (`appcompat-v7`, `design`, `recyclerview-v7`, `cardview-v7`, `support-v4`)
- Gradle Android plugin 2.2.3, build tools 25.0.2
- Third-party libs:
  - [Glide](https://github.com/bumptech/glide) 3.7.0 — image loading/caching
  - [TextDrawable](https://github.com/amulyakhare/TextDrawable) 1.0.1 — letter-avatar icons
  - [MaterialEditText](https://github.com/rengwuxian/MaterialEditText) 2.1.4 — the category-name input
  - [material-dialogs](https://github.com/afollestad/material-dialogs) 0.9.2.3

## Build & run

From the Gradle root (`photo-manager/`):

```bash
cd ../../../../../../../..   # back to photo-manager/
./gradlew assembleDebug      # build the APK
./gradlew installDebug       # install on a connected device/emulator
```

Given the SDK/support-library versions, this builds against a matching legacy Android environment (Android Gradle Plugin 2.x, JDK 8). Modern Android Studio will prompt to migrate the plugin and AndroidX before it can build.

It needs a real camera and external storage, so an emulator with a camera or a physical device is required to actually add photos. Permissions requested: `CAMERA` and `WRITE_EXTERNAL_STORAGE` (read is requested at runtime on API 23+).

## How the pieces fit

| File | Role |
|------|------|
| `MainActivity.java` | Category list, create/delete flow, `CursorLoader` + action mode |
| `ShowImagesActivity.java` | Per-category screen: camera capture, tabs, image loader |
| `MyDatabaseHelper.java` | `SQLiteOpenHelper` — schema and table DDL |
| `MyDataProvider.java` | `ContentProvider` routing category vs. image URIs via `UriMatcher` |
| `MyViewAdapter.java` | Category card adapter, extends `SelectableAdapter` |
| `MyAllImagesViewAdapter.java` | Image grid adapter (Glide) |
| `MyTaggedImagesViewAdapter.java` | Adapter for the tagged view |
| `SelectableAdapter.java` | Multi-select base adapter using `SparseBooleanArray` |
| `MyViewPagerAdapter.java` | Two-tab pager: `AllImagesFragment`, `TaggedImagesFragment` |
| `ScrollingFABBehavior.java` | `CoordinatorLayout.Behavior` that slides the FAB with the app bar |
| `AllImagesFragment.java` / `TaggedImagesFragment.java` | The two tab fragments |

## Notable details

- **One ContentProvider, two tables.** `MyDataProvider` matches `myImages` and `myCategory` paths and dispatches each CRUD call to the right table, calling `notifyChange` so the `CursorLoader`s auto-refresh.
- **Range-aware bulk delete.** `MyViewAdapter.removeItems` sorts selected positions descending, then collapses runs of consecutive indices into `notifyItemRangeRemoved` calls instead of deleting one by one.
- **Photo capture via FileProvider.** `ShowImagesActivity` builds a `content://…/provider` URI through `FileProvider`, hands it to the camera intent as `EXTRA_OUTPUT`, and inserts the resulting file path into the DB on `RESULT_OK`.
- **Image count is denormalized.** After each capture the category's `imageCount` is read, incremented, and written back — it isn't computed from the images table at read time.

## Scope note

This is a learning project — early Android, on the pre-AndroidX support libraries, and it shows. A few rough edges are real and left as-is:

- The Java package is `com.example.anujsharma.manageit` even though the folder path says `sudhanshusingh`; the provider authority has a typo (`magnageit`).
- The "TAGS" tab (`TaggedImagesFragment`) is an empty placeholder; the tag-per-category feature the schema anticipates (`tagName`, `tagCount`) is not wired up in the UI.
- `MyViewAdapter` constructs a bare `new MainActivity()` and holds it unused; `MyTaggedImagesViewAdapter` reads a column by the table-name constant. These are bugs, not features.
- No unit or instrumentation tests beyond the generated `ExampleUnitTest` / `ExampleInstrumentedTest` stubs.

Treat it as a working sample of the classic Android category/photo pattern — Activities, Fragments, RecyclerView, CursorLoader, ContentProvider, SQLite, and Glide — not production code.
