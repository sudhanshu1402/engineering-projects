# Instrumented tests — scientific calculator

Android instrumented tests for the scientific calculator app. This is the `androidTest` source set: tests that run on a real device or emulator, not the local JVM.

## What's here

One file, `ExampleInstrumentedTest.java` — the default test Android Studio generates for a new project. It grabs the app context through `InstrumentationRegistry` and asserts the package name is `com.dataflair.scientificcalc`:

```java
@Test
public void useAppContext() {
    Context appContext = InstrumentationRegistry.getInstrumentation().getTargetContext();
    assertEquals("com.dataflair.scientificcalc", appContext.getPackageName());
}
```

That's a smoke test — it confirms the instrumentation harness wires up against the app under test. It doesn't exercise any calculator logic.

## Stack

- JUnit 4 with the `AndroidJUnit4` runner
- AndroidX Test (`androidx.test.ext.junit`, `androidx.test.platform`)

## Run

From the Gradle project root (the `app` module's parent), with a device or emulator connected:

```
./gradlew connectedAndroidTest
```

## Note

Placeholder scaffolding, not real coverage. The package path here (`com/sudhanshusingh/...`) doesn't match the package declared in the file (`com.dataflair.scientificcalc`) — a leftover from the project being renamed. Real UI/logic tests for the calculator would live in this same source set.
