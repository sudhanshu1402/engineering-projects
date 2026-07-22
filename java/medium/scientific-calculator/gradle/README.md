# gradle/

The Gradle wrapper directory for the [scientific-calculator](../) Android app. Not a project on its own.

## What's in here

- `wrapper/gradle-wrapper.jar` — the small bootstrap jar the `gradlew` scripts run.
- `wrapper/gradle-wrapper.properties` — pins the Gradle version to download and use.

The wrapper lets anyone build the app with the exact Gradle version it was written against, without installing Gradle by hand. Running `./gradlew` (or `gradlew.bat` on Windows) from the project root reads these files, downloads that Gradle version on first run, caches it, and runs the build.

## Pinned version

```
gradle-6.1.1-all.zip
```

Set in `wrapper/gradle-wrapper.properties` via `distributionUrl`. It also stores the distribution under `GRADLE_USER_HOME` so it's shared across projects. The properties file is dated June 2020, matching the Gradle 6.1.1 era.

## Where the actual app lives

The calculator code, build config, and run instructions are one level up:

- `../build.gradle`, `../settings.gradle` — build setup
- `../app/` — the Android module (`MainActivity.java`, layouts, resources)
- `../README.md` — project overview

To build from the project root:

```bash
./gradlew build
```

## Note

Don't edit `gradle-wrapper.jar` by hand. To change the Gradle version, either edit `distributionUrl` in the properties file or run `./gradlew wrapper --gradle-version <x.y.z>`, which regenerates both files.
