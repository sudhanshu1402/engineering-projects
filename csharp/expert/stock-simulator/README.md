# Stock Simulator

A C# console project scaffold for a stock market simulator. Currently a stub.

## Status

Honest heads-up: this isn't implemented yet. `program.cs` is a single `Main` that prints a placeholder line and holds a comment marking where the simulation logic will go. There's no market model, no pricing engine, no portfolio, no tests.

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Stock Market Simulator logic here...");
    // Complex simulation logic stub
}
```

## Run it

```
dotnet run
```

Prints:

```
Stock Market Simulator logic here...
```

The `.replit` file (`run = "dotnet run"`) wires the same command up on Replit.

## Stack

- C# (.NET, run via `dotnet`)
- No external dependencies — no `.csproj` committed here, just the source file and the Replit runner config.

## Scope

Placeholder for a learning exercise. Filed under `csharp/expert` in the engineering-projects collection, but the code doesn't reflect that difficulty yet — it's a starting point, not a finished simulator.
