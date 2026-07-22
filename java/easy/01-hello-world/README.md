# Hello World (Java)

The classic first Java program: print a line of text to the console.

## Status

Placeholder. This directory currently holds only this README — the source file (`HelloWorld.java`) hasn't been added yet. It's slot `01` in the `java/easy` track.

## What it will be

A single class with a `main` method that prints `Hello, World!` to standard output. The point is to confirm a working JDK toolchain and the `compile -> run` loop, nothing more.

## Expected shape

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

## Build & run

Once `HelloWorld.java` exists here:

```bash
javac HelloWorld.java   # produces HelloWorld.class
java HelloWorld         # prints: Hello, World!
```

JDK 11+ can also run a single source file without a separate compile step:

```bash
java HelloWorld.java
```

## Scope

Learning exercise. First entry in the easy Java set.
