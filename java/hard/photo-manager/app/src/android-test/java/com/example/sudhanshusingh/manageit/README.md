# manageit — instrumented tests

Android instrumented (on-device) tests for the `manageit` photo-manager app.

## What's here

One file: `ExampleInstrumentedTest.java`. This is the default test Android Studio generates when you create a project. It runs on a real device or emulator, grabs the app's `Context`, and asserts the package name is `com.example.anujsharma.manageit`. That's it — a smoke test that the app packaging is wired up correctly.

```java
@Test
public void useAppContext() throws Exception {
    Context appContext = InstrumentationRegistry.getTargetContext();
    assertEquals("com.example.anujsharma.manageit", appContext.getPackageName());
}
```

## Stack

- JUnit 4 with the `AndroidJUnit4` runner
- `android.support.test` (the old Android Support test libraries, pre-AndroidX)

## Running

From the project root, with a device or emulator connected:

```
./gradlew connectedAndroidTest
```

Or run the class directly from Android Studio.

## Note

This is boilerplate, not hand-written test coverage — the real logic lives in the app's main source set. The folder is kept because it's part of the standard Android project layout. The package declaration (`com.example.anujsharma.manageit`) still carries the original author's name from when the project was scaffolded.
