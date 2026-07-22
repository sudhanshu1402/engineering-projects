# Hello World (C#)

The classic first program: print a line of text to the console. First entry in the C# easy track.

## Status

Placeholder. There's no source code in this folder yet — just this README. The sibling folders (`console-calculator`, `number-guess`) each hold a `program.cs`; this one is still to be added.

## What it will be

A minimal C# console app that writes `Hello, World!` to standard output. The point is to get a toolchain working end to end: write a file, compile it, run it, see output.

## Expected shape

Once added, the program is one statement:

```csharp
Console.WriteLine("Hello, World!");
```

With top-level statements (C# 9+) that's the whole file. The older form wraps it in a class and `Main`:

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

## Build & run

With the .NET SDK installed:

```bash
dotnet run
```

Or compile a single file directly:

```bash
dotnet run program.cs   # .NET 10+ file-based apps
```

Expected output:

```
Hello, World!
```

## Scope

Learning exercise. Nothing to it beyond confirming the environment works.
