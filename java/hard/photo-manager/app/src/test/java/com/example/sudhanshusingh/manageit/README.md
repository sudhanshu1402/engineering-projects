# manageit — local unit tests

The JVM-side test source set for the `manageit` (photo-manager) Android app. Tests here run on your development machine, not on a device or emulator.

## What's here

- `ExampleUnitTest.java` — the placeholder test Android Studio generates with every new project. One method, `addition_isCorrect()`, asserts `2 + 2 == 4`. It's a smoke test to prove the JUnit toolchain is wired up; no app code is exercised yet.

That's the whole directory. No real unit tests have been written for the app's classes.

## Stack

- JUnit 4.12 (`testCompile 'junit:junit:4.12'` in `app/build.gradle`)
- Plain JVM execution — nothing here depends on the Android framework, so no emulator is needed.

## Run

From the project root:

```bash
./gradlew test
```

That runs everything under `src/test/`. To target just this class:

```bash
./gradlew testDebugUnitTest --tests "*.ExampleUnitTest"
```

## Note on the package name

The declared package in `ExampleUnitTest.java` is `com.example.anujsharma.manageit`, which matches the app's `applicationId` in `build.gradle` — not the `sudhanshusingh` segment in this folder's path. If you ever add real tests, keep the `package` line matching the class under test, not the directory path.

## Scope

This is a stub, not a test suite. Instrumented UI tests (Espresso) would live in a separate `src/androidTest/` source set, which this project doesn't have yet.
