# gradle/ — Gradle wrapper

This is not a project. It's the Gradle wrapper directory for the parent `photo-manager` Android app, and it does one job: pin the exact Gradle version the build uses so anyone can build without installing Gradle first.

## What's in here

| File | Purpose |
|------|---------|
| `wrapper/gradle-wrapper.jar` | Small bootstrap jar (~52 KB) that the `gradlew` / `gradlew.bat` scripts run. It downloads the pinned Gradle distribution if it's not already cached, then hands off the build. |
| `wrapper/gradle-wrapper.properties` | Config for that bootstrap — which Gradle version to fetch and where to cache it. |

## Pinned version

From `gradle-wrapper.properties`:

```
distributionUrl=https\://services.gradle.org/distributions/gradle-2.14.1-all.zip
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
```

So the build uses **Gradle 2.14.1**, downloaded once to `~/.gradle/wrapper/dists` and reused after that. The parent `build.gradle` pairs this with the **Android Gradle plugin 2.2.3** — both are old (the wrapper stamp reads Dec 2015), consistent with a mid-2010s Android project.

## How it's used

You don't run anything in this directory directly. From the parent `photo-manager/` folder:

```bash
./gradlew assembleDebug     # macOS / Linux
gradlew.bat assembleDebug   # Windows
```

`gradlew` reads `gradle-wrapper.properties`, ensures Gradle 2.14.1 is present (fetching via `gradle-wrapper.jar` on first run), and builds the app.

## Note

Committing the wrapper (jar + properties) is the standard, intended setup — it's what makes the build reproducible across machines. There's no source code to read here; the actual app lives in `photo-manager/app/`.
