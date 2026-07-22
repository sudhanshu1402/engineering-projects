# scientificcalc — local unit tests

Local JVM unit tests for the Scientific Calculator Android app. These run on the host machine (no emulator or device needed).

## What's here

Just one file: `ExampleUnitTest.java` — the default test Android Studio generates for a new project. It asserts `2 + 2 == 4` and nothing else:

```java
@Test
public void addition_isCorrect() {
    assertEquals(4, 2 + 2);
}
```

It's a placeholder. It does not test any calculator logic — the actual app code lives under `app/src/main/java/com/sudhanshusingh/`. This test sanity-checks that JUnit is wired up and the test task runs.

## Stack

- JUnit 4.12 (`testImplementation 'junit:junit:4.12'` in `app/build.gradle`)
- Runs as a plain JVM test, not an instrumented Android test

## Run it

From the project root (`scientific-calculator/`):

```bash
./gradlew test
```

That compiles and executes everything under `app/src/test/`.

## Note

Boilerplate. If you're looking for real coverage of the calculator, it isn't here yet — this is the empty starting point that ships with a fresh Android project.
